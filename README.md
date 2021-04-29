# ITXMGL
import java.util.Scanner;//导入java输入流
import java.lang.*;
import java.io.*;
class Student
{
	private static Student[] s=new Student[2];
    int n=0;
	private String name;
	private int num;
	private String classAge;
	
	public void judge()throws IOException
	{
		int i;
		char ch;
		String str;
		Scanner In=new Scanner(System.in);
		if(n==0)
		{
			System.out.print("你还没有录入任何学生，是否录入(Y/N):");
			str=In.next();
			ch=str.charAt(0);
			while(ch!='Y'&&ch!='y'&&ch!='N'&&ch!='n')
			{
				System.out.print("输入有误，请重新输入:");
				str=In.next();
				ch=str.charAt(0);
			}
			if(ch=='Y'||ch=='y')
			{
				this.add();
			}
			if(ch=='N'||ch=='n')
			{
				this.menu();
			}
		}
	}
	
	public void menu()throws IOException//定义菜单函数
	{
		int a;//定义switch语句变量
		Scanner in=new Scanner(System.in);//实例化输入流对象
		System.out.println("*********学生信息管理系统功能表*********");
		System.out.println("*****           1.增加             *****");
		System.out.println("*****           2.显示             *****");
		System.out.println("*****           3.修改             *****");
		System.out.println("*****           4.删除             *****");
		System.out.println("*****           5.查看             *****");
		System.out.println("*****           0.退出             *****");
		System.out.println("****************************************");
		System.out.print("请选择(0~5):");
		a=in.nextInt();
		while(a<0||a>5)
		{
			System.out.print("输入超出范围，请重新输入:");
			a=in.nextInt();
		}
		switch(a)
		{
			case 1:this.add();break;
			case 2:this.show();break;
			case 3:this.modif();break;
			case 4:this.delete();break;
			case 5:this.look();break;
			case 0:System.exit(0);break;
		}			
	}
	
	public void add()throws IOException//定义增加函数
	{
		String str,str1,str2;
		int i,num1,t=1;
		char ch,ch1;
		FileWriter fw=new FileWriter("F://javaFile//student.txt",true);
		fw.write("             录入的学生信息列表\r\n\r\n学号     姓名     班级\r\n");
		Scanner In=new Scanner(System.in);
		while(t==1)
		{
			System.out.print("请输入学生学号:");
			num1=In.nextInt();
			for(i=0;i<n;i++)
			{
				while(s[i].num==num1)
				{
					System.out.println("已存在此学号，请重新输入");
					System.out.print("请输入学号:");
					num1=In.nextInt();
				}
			}
			s[n].num=num1;
			str2=String.valueOf(num1);
			fw.write(str2+"    ");
			System.out.println();
			System.out.print("请输入学生姓名:");
			s[n].name=In.next();
			fw.write(s[n].name+"      ");
			System.out.println();
			System.out.print("请输入学生班级:");
			s[n].classAge=In.next();
			fw.write(s[n].classAge+"\r\n");
			++n;
			fw.close();	
			System.out.println();
			System.out.print("是否继续添加(Y/N)");
			str=In.next();
			ch=str.charAt(0);
			while(ch!='N'&&ch!='n'&&ch!='Y'&&ch!='y')
			{
				System.out.print("输入有误，请重新输入:");
				str=In.next();
				ch=str.charAt(0);
			}
			if(ch=='N'||ch=='n')
			{
				break;
			}
		}
		System.out.println();
		System.out.print("是否返回主菜单(Y/N)");
		str1=In.next();
		ch1=str1.charAt(0);
		while(ch1!='Y'&&ch1!='y'&&ch1!='N'&&ch1!='n')
		{
			System.out.print("输入有误，请重新输入:");
			str1=In.next();
			ch1=str1.charAt(0);
		}
		if(ch1=='Y'||ch1=='y')
		{
			this.menu();
		}
		if(ch1=='N'||ch1=='n')
		{
			System.out.println("正在退出...谢谢使用!");
			System.exit(0);
		}
	}
	
	public void show()throws IOException
	{
		int i;
		this.judge();	
		System.out.println("本次操作共录入"+n+"位学生!");
		System.out.println("你录入的学生信息如下:");
		System.out.println();
		System.out.println("学号\t\t姓名\t班级");
		for(i=0;i<n;i++)                        
		{
			System.out.println(s[i].num+"       "+s[i].name+"      "+s[i].classAge);
		}
		System.out.println("系统返回主菜单!");
		this.menu();
	}
	
	public void delete()throws IOException//删除信息功能实现  注：本功能暂时不具备可扩展性
	{
		this.judge();
		int j=0,t=0,k=0,num1;
		char ch;
		String str;
		Scanner pin=new Scanner(System.in);
		System.out.print("请输入要删除的学号:");
		num1=pin.nextInt();
		for(j=0;j<n;j++)
		{
			if(s[j].num==num1)
			{
				k=1;
				t=j;
			}
		}
		if(k==0)
		{
			System.out.println("对不起！你要删除的学号不存在！");
			System.out.println("系统将返回主菜单！");
			this.menu();
		}
		if(k==1)
		{
			System.out.println("你要删除的学生信息如下:");//打印管理员要删除的学生信息
			System.out.println("学号\t姓名\t班级");//本功能暂时不备扩展性
			System.out.println(s[t].num+"      "+s[t].name+"      "+s[t].classAge);
			System.out.println();
			System.out.print("你确定要删除(Y/N):");
			str=pin.next();
			ch=str.charAt(0);
			while(ch!='Y'&&ch!='y'&&ch!='N'&&ch!='n')
			{
				System.out.print("输入有误，请重新输入:");
				str=pin.next();
				ch=str.charAt(0);
			}
			if(ch=='N'||ch=='n')
			{
				System.out.println();
				System.out.println("系统返回主菜单！");
				this.menu();
			}
			if(ch=='Y'||ch=='y')
			{
				for(j=t;j<n-1;j++)
				{
					s[j]=s[j+1];
				}
				n--;
				System.out.println("数据成功删除!");
				System.out.println("系统返回主菜单!");
				this.menu();
			}
		}
	}
