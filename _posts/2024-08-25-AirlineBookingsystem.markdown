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
+ This code is about connect with database and create the table. For deal with sql in java, you need to use try and catch.
+ What If you didn't get success, please check your schema name and password.  
+ *The result of creating database. Successfully get this information*
<img width="250" alt="Screenshot 2024-09-16 at 7 35 05 PM" src="https://github.com/user-attachments/assets/8a5a4dcf-e2f6-4638-95ea-7dbd1d3d37a2">  

## The code below is the first screen of this project.
```java
package Book_seat;

import java.awt.Color;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;

public class CountrySelect extends JFrame  {	
	
public JButton []country = new JButton [5];
public JButton[] Pin = new JButton[5];

public CountrySelect() {

	setSize(600, 850);
	setTitle("packagetour_countryselect");
	setLocationRelativeTo(null);

	JPanel upper = new JPanel();
	upper.setLayout(null);
	upper.setBackground(new Color(124, 210, 255));

	Pin[0] = new JButton();
	Pin[1] = new JButton();
	Pin[2] = new JButton();
	Pin[3] = new JButton();
	Pin[4] = new JButton();

	Pin[0].setBounds(490, 82, 25, 42);
	Pin[1].setBounds(169, 185, 25, 42);
	Pin[2].setBounds(521, 223, 25, 42);
	Pin[3].setBounds(284, 60, 25, 42);
	Pin[4].setBounds(307, 222, 25, 42);

	for (int i = 0; i < 5; i++) {
		ImageIcon p = new ImageIcon("icon/Pin.png");
		Pin[i].setIcon(p);
		Pin[i].setOpaque(true);
		Pin[i].setBorderPainted(false); //Mac default
		Pin[i].setBorderPainted(false);
		Pin[i].setFocusPainted(false);
		Pin[i].setContentAreaFilled(false);
		upper.add(Pin[i]);
	}

	Pin[0].addActionListener(new ActionListener() {
		@Override
		public void actionPerformed(ActionEvent e) {
			new SelectAirportK();
			setVisible(false); 
		}
	});

	JLabel map = new JLabel();
	ImageIcon worldmap = new ImageIcon("icon/World 2.png");
	map.setIcon(worldmap);
	map.setBounds(0, 10, 600, 300);
	upper.add(map);

	country[0] = new JButton();
	ImageIcon Korea = new ImageIcon("icon/K.png");
	country[0].setIcon(Korea);
	country[1] = new JButton();
	ImageIcon Brazil = new ImageIcon("icon/B.png");
	country[1].setIcon(Brazil);
	country[2] = new JButton();
	ImageIcon Australia = new ImageIcon("icon/A.png");
	country[2].setIcon(Australia);
	country[3] = new JButton();
	ImageIcon Germany = new ImageIcon("icon/G.png");
	country[3].setIcon(Germany);
	country[4] = new JButton();
	ImageIcon Africa = new ImageIcon("icon/R.png");
	country[4].setIcon(Africa);

	country[0].setBounds(50, 350, 500, 60);
	country[1].setBounds(50, 430, 500, 60);
	country[2].setBounds(50, 510, 500, 60);
	country[3].setBounds(50, 590, 500, 60);
	country[4].setBounds(50, 670, 500, 60);

	for (int i = 0; i < country.length; i++) {
		country[i].setOpaque(true);
		country[i].setBorderPainted(false); 
		country[i].setBorderPainted(false);
		country[i].setFocusPainted(false);
		country[i].setContentAreaFilled(false);
		upper.add(country[i]);
	}

	country[0].addActionListener(new ActionListener() {
		@Override
		public void actionPerformed(ActionEvent e) {
			new SelectAirportK();
			setVisible(false);
		}
	});

	add(upper);
	setVisible(true);

}

public static void main(String[] args) {
	CountrySelect test = new CountrySelect();

}
}
```
**This is the image of that code**
<img width="594" alt="Screenshot 2024-09-16 at 7 43 25 PM" src="https://github.com/user-attachments/assets/b32c7ceb-c726-4d9c-8376-92b6a40bb8e1">
