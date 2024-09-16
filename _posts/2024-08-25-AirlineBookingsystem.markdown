---
layout: post
title:  "[Project] Airline Booking System"
date:   2024-08-25 18:03:36 +0900
categories: Java
---

## Description
1. Connect your Java with Mysql. You can check how to link is [here](https://s2se.github.io/posts/Mysql/)
2. Check your connection  
3. Make your table

```java
package manage_db;

import java.sql.Connection;
import java. sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class bookingdb{

	String url = "jdbc:mysql://localhost:3306/yourdbname?useUnicode=true&characterEncoding=UTF-8";
	String id = "root";
	String pw = "password";
	Connection connect;
	Statement stmt ;
	
	public static void main(String[] args) {
		bookingdb db = new bookingdb();
		try {
			db.connect = DriverManager.getConnection( db.url, db.id, db.pw);
			db.stmt = db.connect.createStatement();
			db.make_table();
			System.out.println("success");
		}
		catch(SQLException sql_Ex){
			System.out.println(sql_Ex);
		}
	}
	void make_table(){
		try {
				String createStr ="CREATE TABLE booking_list("
								  +"id varchar(20) not null," 
						          + "`from` varchar(10) not null," 
								  + "`to` varchar(10) not null,"
						          + "PRIMARY KEY(id))";
				stmt.execute(createStr);
				System.out.println("Success to create table");
			}
		catch(Exception e){
				System.out.println("failed to create table" + "because"+ e);
			}
		}
	}


```  
This code is about connect with database and create the table. For deal with sql in java, you need to use try and catch.
What If you didn't get success, please check your schema name and password.  
*The result of creating database. Successfully get this information*
<img width="250" alt="Screenshot 2024-09-16 at 7 35 05 PM" src="https://github.com/user-attachments/assets/8a5a4dcf-e2f6-4638-95ea-7dbd1d3d37a2">

```java

```