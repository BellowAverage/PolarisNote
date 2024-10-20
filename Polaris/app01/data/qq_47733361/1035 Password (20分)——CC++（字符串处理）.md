
--- 
title:  1035 Password (20分)——C/C++（字符串处理） 
tags: []
categories: [] 

---
To prepare for PAT, the judge sometimes has to generate random passwords for the users. The problem is that there are always some confusing passwords since it is hard to distinguish 1 (one) from l (L in lowercase), or 0 (zero) from O (o in uppercase). One solution is to replace 1 (one) by @, 0 (zero) by %, l by L, and O by o. Now it is your job to write a program to check the accounts generated by the judge, and to help the juge modify the confusing passwords.

### Input Specification:

Each input file contains one test case. Each case contains a positive integer N (≤1000), followed by N lines of accounts. Each account consists of a user name and a password, both are strings of no more than 10 characters with no space.

### Output Specification:

For each test case, first print the number M of accounts that have been modified, then print in the following M lines the modified accounts info, that is, the user names and the corresponding modified passwords. The accounts must be printed in the same order as they are read in. If no account is modified, print in one line There are N accounts and no account is modified where N is the total number of accounts. However, if N is one, you must print There is 1 account and no account is modified instead.

### Sample Input 1:

```
3
Team000002 Rlsp0dfa
Team000003 perfectpwd
Team000001 R1spOdfa

```

### Sample Output 1:

```
2
Team000002 RLsp%dfa
Team000001 R@spodfa

```

### Sample Input 2:

```
1
team110 abcdefg332

```

### Sample Output 2:

```
There is 1 account and no account is modified

```

### Sample Input 3:

```
2
team110 abcdefg222
team220 abcdefg333

```

### Sample Output 3:

```
There are 2 accounts and no account is modified

```

### 题目大意：

给定n个人的账号密码，如果密码中包含‘1’，‘0’，‘l’，‘O’，则按如下规则变换：
1. ‘1’变为‘@’；1. ‘0’变为‘%’；1. ‘l’变为‘L’；1. ‘O’变为‘o’。
最后按输入顺序输出变换过的账号与密码；如果没有需要变换的则输出一句话，注意单复数。

### 思路及分析：

定义一个结构体存储账户信息，在输入的同时修改密码并统计需要修改的账户个数，最后遍历结构体即可得到想要的结果。

### AC代码：

```
#include&lt;iostream&gt;
#include&lt;string&gt;

using namespace std;
struct Node{<!-- -->
	string name, password;
	bool flag;
}a[1010];

int main(){<!-- -->
	int n, t = 0;
	cin &gt;&gt; n;
	for(int i = 0; i &lt; n; i++){<!-- -->
		cin &gt;&gt; a[i].name &gt;&gt; a[i].password;
		for(int j = 0; j &lt; a[i].password.length(); j++){<!-- -->
			if(a[i].password[j] == '1') a[i].password[j] = '@', a[i].flag = true;
			if(a[i].password[j] == '0') a[i].password[j] = '%', a[i].flag = true;
			if(a[i].password[j] == 'l') a[i].password[j] = 'L', a[i].flag = true;
			if(a[i].password[j] == 'O') a[i].password[j] = 'o', a[i].flag = true;
		}
		if(a[i].flag == true) t++;
	}
	if(!t){<!-- -->
		if(n == 1) cout &lt;&lt; "There is 1 account and no account is modified" &lt;&lt; endl;
		else cout &lt;&lt; "There are " &lt;&lt; n &lt;&lt;" accounts and no account is modified" &lt;&lt; endl;
	}else{<!-- -->
		cout &lt;&lt; t &lt;&lt; endl;
		for(int i = 0; i &lt; n; i++){<!-- -->
			if(a[i].flag == true){<!-- -->
				cout &lt;&lt; a[i].name &lt;&lt; ' ' &lt;&lt; a[i].password &lt;&lt; endl;
			}
		}
	}
	return 0;
}

```
