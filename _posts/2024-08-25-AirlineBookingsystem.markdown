---
layout: post
title:  "[Project] Airline Booking System"
date:   2024-08-25 18:03:36 +0900
categories: Java
---

## Description
1. Connect your Java with Mysql. You can check how to link is [here](https://s2se.github.io/posts/Mysql/)
2. Check your connection 
```java
import java.sql.Connection;
import java. sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class check_connec{
	
	public static void main(String[] args) {
		String url = "jdbc:mysql://localhost:3306/DBname?useUnicode=true&characterEncoding=UTF-8";
		
		try {
			Connection connect = DriverManager.getConnection( url, "root","yourpassword");
			System.out.println("success");
			Statement stmt = connect.createStatement();
		}
		catch(SQLException sql_Ex){
			System.out.println(sql_Ex);
		}
	}
}

```
If you got a message "success" then you can use mysql with Java. If not, please check your schema name and password.
From url, after localhost:3306, you need to put your dbname. 
