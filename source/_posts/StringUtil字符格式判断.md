---
title: StringUtil字符格式判断
categories: Java
cover: lab/img/cover4.webp
top_img: https://cdn.jsdelivr.net/gh/runrab/cdn2@master/img/mid/acg/acg122.jpeg
abbrlink: 1237
date: 2020-09-19 09:08:41
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
---

## StringUtil 字符格式判断

```
 java 字符串格式检验

将以逗号分隔的字符串转换成字符串数组

获取字符串编码

判断字符串是否为数字

判断是否是数字(整数)

判断是否是邮箱

是否是汉字
```

```java
package com.ssh.insure.utils;
 
import java.util.regex.Matcher;
import java.util.regex.Pattern;
 
/**
 * 字符串相关方法
 *
 */
public class StringUtil {
 
	/**
	 * 将以逗号分隔的字符串转换成字符串数组
	 * @param valStr
	 * @return String[]
	 */
	public static String[] StrList(String valStr){
	    int i = 0;
	    String TempStr = valStr;
	    String[] returnStr = new String[valStr.length() + 1 - TempStr.replace(",", "").length()];
	    valStr = valStr + ",";
	    while (valStr.indexOf(',') > 0)
	    {
	        returnStr[i] = valStr.substring(0, valStr.indexOf(','));
	        valStr = valStr.substring(valStr.indexOf(',')+1 , valStr.length());
	        
	        i++;
	    }
	    return returnStr;
	}
	
	/**获取字符串编码
	 * @param str
	 * @return
	 */
	public static String getEncoding(String str) {      
	       String encode = "GB2312";      
	      try {      
	          if (str.equals(new String(str.getBytes(encode), encode))) {      
	               String s = encode;      
	              return s;      
	           }      
	       } catch (Exception exception) {      
	       }      
	       encode = "ISO-8859-1";      
	      try {      
	          if (str.equals(new String(str.getBytes(encode), encode))) {      
	               String s1 = encode;      
	              return s1;      
	           }      
	       } catch (Exception exception1) {      
	       }      
	       encode = "UTF-8";      
	      try {      
	          if (str.equals(new String(str.getBytes(encode), encode))) {      
	               String s2 = encode;      
	              return s2;      
	           }      
	       } catch (Exception exception2) {      
	       }      
	       encode = "GBK";      
	      try {      
	          if (str.equals(new String(str.getBytes(encode), encode))) {      
	               String s3 = encode;      
	              return s3;      
	           }      
	       } catch (Exception exception3) {      
	       }      
	      return "";      
	   } 
	/**
	 * 判断字符串是否为数字
	 * @param str
	 * @return
	 */
	public static boolean isNumeric(String str) {  
		java.util.regex.Pattern pattern=java.util.regex.Pattern.compile("^(([1-9]{1}\\d*)|([0]{1}))(\\.(\\d){0,2})?$"); // 判断小数点后2位的数字的正则表达式
        java.util.regex.Matcher match=pattern.matcher(str); 
        if(match.matches()){ 
            return true; 
        }else{ 
        	return false;
        } 
	}
	 /**
     * 判断是否是数字(整数)
     * @param str
     * @return
     */
    public static boolean isNumericINT(String str){ 
	   Pattern pattern = Pattern.compile("[0-9]*"); 
	   Matcher isNum = pattern.matcher(str);
	   if(isNum.matches()){
		   return true; 
	   } 
	   return false; 
	   
    }
    /**
     * 判断是否是邮箱
     * @param string
     * @return
     */
    public static boolean isEmail(String string) {
        if (string == null)
            return false;
        String regEx1 = "^[a-zA-Z0-9_.-]+@[a-zA-Z0-9-]+(\\.[a-zA-Z0-9-]+)*\\.[a-zA-Z0-9]{2,6}$";
        Pattern p;
        Matcher m;
        p = Pattern.compile(regEx1);
        m = p.matcher(string);
        if (m.matches())
            return true;
        else
            return false;
    }
    /**
     * 是否是汉字
     * @param string
     * @return
     */
    public static boolean isChinese(String string) {
    	String regEx = "[\u4e00-\u9fa5]";
		Pattern pat = Pattern.compile(regEx);
		Matcher matcher = pat.matcher(string);
		boolean flg = false;
		if (matcher.find())
			flg = true;
 
		return flg;
    }
    
}
```

