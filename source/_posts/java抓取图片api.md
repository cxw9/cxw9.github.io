---
title: java抓取图片api
categories: Java
cover: lab/img/cover1.webp
abbrlink: 59659
date: 2020-11-29 21:23:16
updated:
tags:
keywords:
description:
comments:
toc:
toc_number:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
swiper_index: 5
swiper_desc: 
swiper_cover: 
---

```java
package demo;

import javax.net.ssl.HttpsURLConnection;
import java.io.*;
import java.net.URL;
import java.net.URLConnection;
import java.net.URLEncoder;
import java.nio.charset.Charset;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.HashSet;
import java.util.Scanner;
import java.util.Set;

// https://api.mtyqx.cn/api/random.php（二次元动漫）

//https://api.mtyqx.cn/tapi/random.php（二次元动漫）

public class getImg {
    public static void main(String[] args) throws Exception {
        Scanner scan=new Scanner(System.in);
        System.out.println("输入开始-----换行输入");
        int ifDownload=0;
        System.out.println("输入0选择位置下载");
        ifDownload=scan.nextInt();//输入0选择位置下载
        String inUrl;
        String inImgFilTmpPath;
        String inImgFilPath;
        String downPath;
        int inNumber;
        if(ifDownload!=0){
            System.out.println("随机url api地址:"+"https://api.ixiaowai.cn/mcapi/mcapi.php"); inUrl="https://tools.pursuewind.com/acgPic";
            System.out.println("随机url 存放地址:"+"D:\\tmp\\img\\img-tmp.txt");       inImgFilTmpPath="D:\\tmp\\img\\img-tmp.txt";
            System.out.println("随机url 去重存放地址:"+"D:\\tmp\\img\\img.txt");        inImgFilPath="D:\\tmp\\img\\img.txt";
            System.out.println("随机url 本地下载位置:"+"D:\\\\tmp\\\\img\\\\acg");      downPath="D:\\\\tmp\\\\img\\\\acg";
            System.out.println("下载数量"+"50");                                      inNumber=50;
        } else{
            System.out.print("随机url api地址:");      inUrl = scan.nextLine();
            System.out.print("随机url 存放地址:");      inImgFilTmpPath = scan.nextLine();
            System.out.print("随机url 去重存放地址:");   inImgFilPath = scan.nextLine();
            System.out.print("随机url 本地下载位置:");   downPath = scan.nextLine(); //下载位置
            System.out.print("下载数量");               inNumber=scan.nextInt();
        }
        System.out.print("是否下载,默认不下载0，输入1下载:");
        int down_or=0;
        down_or=scan.nextInt();
        // FileOutputStream fos = new FileOutputStream(file,true);
        //void write(int b)：将指定的字节写入此文件输出流
        // TODO 自动生成的方法存根
        long start=System.currentTimeMillis();
        //existFile(inImgFilTmpPath,inImgFilPath,downPath);    //文件存在判断
        System.out.println("获取链接开始");
        //路径存在判断
        existFile(inImgFilTmpPath,inImgFilPath,downPath);
        //得到图片链接
        getImgUrl(inUrl,inImgFilTmpPath,inNumber);
        delete(inImgFilTmpPath,inImgFilPath);//去重
        returnImg(inImgFilTmpPath,inImgFilPath );//回写
        /**
         if(down_or==1){
         download(downPath,inImgFilPath); //下载
         }else{
         System.out.println("本次未下载");
         }
          */
        //download(downPath,inImgFilPath);
        newDownload(downPath,inImgFilPath);
        long end=System.currentTimeMillis();
        System.out.println("运行时间:"+(end-start)/1000+"秒");
    }

    public static void delete( String inImgFilTmpPath,String inImgFilPath) throws IOException {
        File file=new File(inImgFilPath);
        FileOutputStream out1=new FileOutputStream(file,false);
        BufferedReader br = null;
        FileReader reader = null;
        String str = null;
        //去重后数量
        int count =0;
        //去重数量
        int sum=0;
        Set<String> e_types = new HashSet<String>();
        System.out.println("本地去重开始");
        reader = new FileReader(inImgFilTmpPath);//必须是https协议
        br = new BufferedReader(reader);
        while ((str = br.readLine()) != null) {
            if(e_types.add(str)) {
                byte[] bys = (str+"\n").getBytes();
                out1.write(bys);
                count ++;
                //System.err.println(str);
            }else {
                sum++;
            }
        }
        br.close();
        reader.close();
        out1.close();
        System.out.println("本地去重完成 共 "+count+"个"+"去重 " +sum+" 个");
    }

    //得到图片链接
    public static  void getImgUrl(String inUrl,String inImgFilTmpPath,int inNumber) throws FileNotFoundException {
        File file = new File(inImgFilTmpPath);
        int badsum=0;
        for(int i=1;i<=inNumber;i++) {
            FileOutputStream fos = new FileOutputStream(file,true);
            String url1=inUrl;
            try {
                URL url = new URL(url1);
                HttpsURLConnection conn = (HttpsURLConnection) url.openConnection();
                //解决403请求
                conn.addRequestProperty("User-Agent", "Mozilla/4.76");
                conn.setRequestMethod("GET");//请求方式
                conn.setConnectTimeout(5*1000);//连结过时时间
                //connection.setReadTimeout(5000); // 5秒 从主机读取数据的超时时间（单位：毫秒）
                InputStream in = conn.getInputStream();
                //得到真实连接
                //System.out.println(conn.getURL());
                /**方法一
                 * */
                //得到真实连接
                String s=conn.getURL().toString()+"\n";
                //转换byte[]写入
                byte[] bys = s.getBytes();
                fos.write(bys);
                fos.close();
            } catch (IOException e) {
                // TODO 自动生成的 catch 块
                //e.printStackTrace(); //可注释掉本行不显示错误信息
                badsum++;
                //break;//错误时终止循环
            }
        }

        System.out.println("bad链接 "+badsum);
    }
    //回写
    public static void returnImg(String inImgFilTmpPath,String inImgFilPath ) throws IOException {
        //File file=new File("resource\\图片链接\\demo\\acg.txt");
        //FileInputStream fishuixie = new FileInputStream(file);
        //FileOutputStream foshuixie=new FileOutputStream("resource\\图片链接\\demo\\acg-tmp.txt",false);
        System.out.println("回写开始");
        File f =new File(inImgFilPath);
        BufferedReader lineNumberReader = null;
        StringBuffer buffer = null;
        try {
            lineNumberReader= new BufferedReader(new FileReader(f));
            buffer = new StringBuffer();
            String  temp = "";
            while ((temp=lineNumberReader.readLine())!=null){
                buffer.append(temp).append("\n");
            }
            //System.out.println(buffer.toString());
        }catch (IOException e){
            e.printStackTrace();
        }finally {
            try {
                lineNumberReader.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        File file = null;
        file =new File(inImgFilTmpPath);
        FileOutputStream fos =null;
        try {
            if (!file.exists()){
                file.createNewFile();
            }
            fos = new FileOutputStream(file);
            fos.write(buffer.toString().getBytes());
        }catch (IOException e){
            e.printStackTrace();
        }finally {
            try {
                fos.close();
            } catch (IOException e) {
                e.printStackTrace(); }
        }
        System.out.println("回写完成");
    }
    //文件存在判断
    public static void  existFile( String inImgFilTmpPath,String inImgFilPath,String downPath) throws IOException {
        File file1=new File(inImgFilTmpPath);
        File file2=new File(inImgFilPath);
        File file3=new File(downPath);

        if( file1.exists()&&file1.isFile()){
            //System.out.println("文件已经存在---正常");
        }else {
            file1.createNewFile();
            System.out.println("文件不存在---帮你创建");
        }
        if( file2.exists()&&file2.isFile()){
            //System.out.println("url存放文件已经存在---正常");
        }else {
            file2.createNewFile();
            System.out.println("url存放文件不存在---帮你创建");
        }
        if( file3.exists()&&file3.isDirectory()){
            //System.out.println("下载目录已经存在---正常");
        }else {
            file3.mkdirs();
            System.out.println("下载目录不存在---帮你创建");
        }
    }
    //图片下载时不下载已经存在的
    //默认值不用手动输入
    //下载进度条
    // 进度条粒度
    private static String getNChar(int num, char ch){
        StringBuilder builder = new StringBuilder();
        for(int i = 0; i < num; i++){
            builder.append(ch);
        }
        return builder.toString();
    }
    public static void progressBar()throws InterruptedException {
        int index = 0;
        String finish;
        String unFinish;
        final int PROGRESS_SIZE = 50;
        int BITE = 2;
        System.out.print("Progress:");
        finish = getNChar(index / BITE, '█');
        unFinish = getNChar(PROGRESS_SIZE - index / BITE, '─');
        String target = String.format("%3d%%[%s%s]", index, finish, unFinish);
        System.out.print(target);
        while (index <= 100){
            finish = getNChar(index / BITE, '█');
            unFinish = getNChar(PROGRESS_SIZE - index / BITE, '─');
            target = String.format("%3d%%├%s%s┤", index, finish, unFinish);
            System.out.print(getNChar(PROGRESS_SIZE + 6, '\b'));
            System.out.print(target);
            Thread.sleep(50);
            index++;
        }
    }
    //新的下载方法
    public static void newDownload(String downPath,String inImgFilPath) throws InterruptedException {
        System.out.println("下载开始");
        int sum_img_url=0;//本地已经有的图片 重复不用下载数量
        //int barNum=0;//进度条终点
        //int start_num=1;//实时进度 防止取0错误
        //int posNum=0;//百分进度判断位置
        //int hang=1;//当前行数
        Path path = Paths.get(inImgFilPath);//JDK7引入path
        Charset charset = Charset.forName("US-ASCII");
        try (BufferedReader reader = Files.newBufferedReader(path, charset)) {
            String line = null;
            while ((line = reader.readLine()) != null) {
                //System.out.println(line);
                //hang++;
                DownloadNewFile(downPath,line);
                /**
                 start_num=(int) ((100*hang)/getFileLineNum(inImgFilPath));
                 if(start_num<1){start_num=1;
                 }else{ start_num=(int) ((100*hang)/getFileLineNum(inImgFilPath));
                 }
                 */
                //bar_progress(start_num);//进度数字
            }
        } catch (IOException x) {
            System.err.format("IOException: %s%n", x);
        }
        //(int) ((100*hang)/getFileLineNum(inImgFilPath))
        // progressBar();
    }
   //Java获取文件的行数
    public static long getFileLineNum(String filePath) {
        try {
            return Files.lines(Paths.get(filePath)).count();
        } catch (IOException e) {
            return -1;
        }
    }
    //   新的实际下载方法
    public static void DownloadNewFile(String filePath,String sImgUrl) throws IOException {
        URL url = new URL(sImgUrl); //获取图片URL
        URLConnection connection = url.openConnection(); //获得连接
        //截取图片文件名
        String fileName = sImgUrl.substring(sImgUrl.lastIndexOf('/') + 1, sImgUrl.length());
        // 文件名里面可能有中文或者空格，所以这里要进行处理。但空格又会被URLEncoder转义为加号
        String urlTail = URLEncoder.encode(fileName, "UTF-8");// 因此要将加号转化为UTF-8格式的%20
        //如果没图片格式是 文件名前缀
        sImgUrl = sImgUrl.substring(0, sImgUrl.lastIndexOf('/') + 1) + urlTail.replaceAll("\\+", "\\%20");
        String suffix=connection.getContentType();//文件名后缀
        //System.out.println(sImgUrl);
        //写出路径
        File file = new File(filePath + File.separator + fileName);
        if (file.exists()){
            //System.out.println("文件存在");
        }else{
            try {
                //URL url = new URL(sImgUrl); //获取图片URL
                //URLConnection connection = url.openConnection(); //获得连接
                connection.setConnectTimeout(5 * 1000); //设置5秒的响应时间
                connection.addRequestProperty("User-Agent", "Mozilla/4.76");//解决403请求
                //connection.getContentType();//获取文件类型
                //System.out.println(connection.getContentType());
                InputStream in = connection.getInputStream();            //获得输入流
                BufferedOutputStream out = new BufferedOutputStream(new FileOutputStream(file));//获得输出流
                byte[] buf = new byte[8192];//1024改为8192 //构建缓冲区
                int size;
                //写入到文件
                while (-1 != (size = in.read(buf))) { out.write(buf, 0, size);}
                out.close(); in.close();
            } catch (IOException e) { e.printStackTrace(); }
         }
        }
    //数字bar
    public static void bar_progress(int start_num) throws InterruptedException {
        System.out.print("Progress:");
        for (;start_num <= 100; start_num++) {
            System.out.print(start_num + "%");
            //Thread.sleep(50);
            for (int j = 0; j <= String.valueOf(start_num).length(); j++) {
                System.out.print("\b");
            }
        }
        System.out.println();
    }
}


/**java 读取文本行数
 public static long getFileLineNum(String filePath) {
 try {
 return Files.lines(Paths.get(filePath)).count();
 } catch (IOException e) {
 return -1;
 }
 }
 */

/**
//下载图片  //https://blog.csdn.net/milletguo/article/details/80144290  这个方法好
public static void  download(String downPath,String inImgFilPath) throws IOException, InterruptedException {
    System.out.println("下载开始");
    int sum_img_url=0;//本地已经有的图片 重复不用下载数量
    int barNum=0;//进度条终点
    //File file = new File("D:\\新建文本文档.txt");// Text文件
    FileReader file=new FileReader(inImgFilPath);//获取文件流
    BufferedReader br = new BufferedReader(file);// 构造一个BufferedReader类来读取文件
    //图片下载时不下载已经存在的
    //File downloadedpath=new File(downPath);
    //File[] array = downloadedpath.listFiles(); //图片下载时不下载已经存在的
    String  sImgUrl=null;
    while ((sImgUrl = br.readLine()) != null) {// 使用readLine方法，一次读一行
        downImages(downPath,sImgUrl);//图片链接不存在下载
        //barNum++;//进度条长度
    }
    br.close();;
    progressBar();
    System.out.println("本地下载结束-重复不用下载数量:"+sum_img_url);
}
*/
/**
    //实际下载图片方法 此处的 sImgUrl 为从文件读取出来的 此处的downPath 对应downPath
    private static void downImages(String filePath, String sImgUrl) {
        //截取图片文件名
        String fileName=sImgUrl.substring(sImgUrl.lastIndexOf('/')+1,sImgUrl.length());
        try {
            // 文件名里面可能有中文或者空格，所以这里要进行处理。但空格又会被URLEncoder转义为加号
            String urlTail = URLEncoder.encode(fileName, "UTF-8");
            // 因此要将加号转化为UTF-8格式的%20
            sImgUrl = sImgUrl.substring(0, sImgUrl.lastIndexOf('/') + 1) + urlTail.replaceAll("\\+", "\\%20");
        } catch (UnsupportedEncodingException e) {
            e.printStackTrace();
        }
        //写出路径
        File file=new File(filePath+File.separator+fileName);
        try {
            //获取图片URL
            URL url=new URL(sImgUrl);
            //获得连接
            URLConnection connection=url.openConnection();
            //设置5秒的响应时间
            connection.setConnectTimeout(5*1000);
            //解决403请求
            connection.addRequestProperty("User-Agent", "Mozilla/4.76");
            //获得输入流
            InputStream in=connection.getInputStream();
            //获得输出流
            BufferedOutputStream out=new BufferedOutputStream(new FileOutputStream(file));
            //构建缓冲区
            byte[] buf=new byte[8192];//1024改为8192
            int size;
            //写入到文件
            while (-1!=(size=in.read(buf))) {
                out.write(buf,0,size);
            }
            out.close();
            in.close();
        }  catch (IOException e) {
            e.printStackTrace();
        }
    }
*/
```

