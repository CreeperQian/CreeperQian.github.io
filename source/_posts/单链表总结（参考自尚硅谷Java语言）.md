---
title: 单链表总结（参考自尚硅谷Java语言）
date: 2020-10-06 01:24:32
tags:
- 数据结构与算法
- 技术
- 尚硅谷
- JAVA
categories:
- 技术
author: Creeper
img: https://creeper-1303839585.cos.ap-beijing.myqcloud.com/blog/Single%20Linked%20List%20%20summary/1.jpg
---
***参考自尚硅谷***
*单链表可以有头节点也可以没有。*
**以下代码涵盖单链表的总结。**
## 英雄排行功能

```java
package com.creeper.linkedlist;

public class SingleLinkedListDemo {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		SingleLinkedList s =new SingleLinkedList();
		HeroNode hero1 = new HeroNode(1, "宋江", "及时雨");
		HeroNode hero2 = new HeroNode(2, "卢俊义", "玉麒麟");
		HeroNode hero3 = new HeroNode(3, "吴用", "智多星");
		HeroNode hero4 = new HeroNode(4, "林冲", "豹子头");
		s.add(hero1);
		s.add(hero4);
		s.add(hero2);
		s.add(hero3);
		s.list();
		SingleLinkedList.reversetList(hero1);
		s.list();
	}
}
//英雄类
class HeroNode{
	public int id;
	public String name;
	public String nickName;
	public HeroNode next;
	public HeroNode(int id, String name,String nickName) {
		this.id = id;
		this.name = name;
		this.nickName = nickName;
	}
	@Override
	public String toString() {
		return "HeroNode [id=" + id + ", name=" + name + ", nickName=" + nickName + "]";
	}
}
//链表类
class SingleLinkedList{
	HeroNode head = new HeroNode(0,"","");
	public HeroNode getHead() {
		return head;
	}
	//显示链表方法
	public void list() {
		if(head.next == null) {
			System.out.println("链表空，无法显示。");
			return;
		}
		HeroNode temp = head;
		while(true) {
			if(temp.next == null) 
				break;
			temp = temp.next;
			System.out.println(temp);
		}
	}
	//无顺序添加链表
	public void add(HeroNode heroNode) {
		HeroNode temp = head;
		while(true) {
			if(temp.next == null)
				break;
			temp = temp.next;
		}
		temp.next = heroNode;
	}
	//按id大小顺序，从小到大，插入或添加链表
	public void addByOrder(HeroNode heroNode) {
		HeroNode temp = head;
		boolean flag = false;
		while(true) {
			if(temp.next == null)
				break;
			if(temp.next.id > heroNode.id)
				break;
			if(temp.next.id == heroNode.id) {
				flag = true;
				break;
			}	
			temp = temp.next;
		}
		if(flag)
			System.out.println("添加失败，已保存目标id。");
		else {
			heroNode.next = temp.next;
			temp.next = heroNode;
		}
	}
	//更新数据
	public void update(HeroNode newHeroNode) {
		if(head.next == null) {
			System.out.println("链表空~");
			return;
		}
			HeroNode temp = head.next;
			boolean flag = false;
			while(true) {
				if(temp.next == null)
					break;
				if(temp.id == newHeroNode.id) {
					flag = true;
					break;
				}
				temp = temp.next;
			}
			if(flag) {
				temp.name = newHeroNode.name;
				temp.nickName = newHeroNode.name;
			} else {
				System.out.println("未找到该节点。");
			}
		}
	//删除英雄
	public void delete(int id) {
		if(head.next == null) {
			System.out.println("链表空~");
			return;
	}
		HeroNode temp = head;
		boolean flag = false;
		while(true) {
			if(temp.next == null)
				break;
			if(temp.next.id == id) {
				flag = true;
				break;
			}
			temp = temp.next;
		}
		if(flag) {
			temp.next =temp.next.next;
		} else {
			System.out.println("未找到该节点。");
		}
	}
	//求有效节点个数
	public static int getLength(HeroNode head) {
		HeroNode temp = head;
		int num = 0;
		while(temp.next != null) {
			temp = temp.next;
			num++;
		}
		return num;
	}
}	
```
## 新浪面试题
```java
//新浪面试题：查找单链表的倒数第k个节点
	public static HeroNode findLastIndexNode(HeroNode head,int index) {
		if(head.next == null) {
			return null;
		}
		int length = SingleLinkedList.getLength(head);
		HeroNode cur = head.next;
		for (int i = 0; i < length - index; i++) {
			cur = cur.next;
		}
		return cur;
	}
```
## 腾讯面试题
```java
	//腾讯面试题：将单链表反转
	public static void reversetList(HeroNode head) {
		if(head.next == null || head.next.next == null) {
			return;
		}
		HeroNode cur = head.next;
		HeroNode next = null;
		HeroNode reverseHead = new HeroNode(0, "", "");
		while(cur != null) {
			next = cur.next;
			cur.next = reverseHead.next;
			reverseHead.next = cur;
			cur = next;
		}
		head.next = reverseHead.next;
	}
```

**以上内容若有错误或更优解，欢迎指正~~。**