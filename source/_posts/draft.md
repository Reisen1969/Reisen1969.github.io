---
title: draft
date: 2023-08-27 19:26:01
tags: draft
toc: true
---



riscv 内核系统调用定义的文件 `linux/include/uapi/asm-generic/unistd.h`

<!-- more -->

## 为riscv内核添加系统调用的方法

直接把 diff 打出来看看.

```


diff --git a/include/linux/syscalls.h b/include/linux/syscalls.h
index 33a0ee3bcb2e..b40451a71d49 100644
--- a/include/linux/syscalls.h
+++ b/include/linux/syscalls.h
@@ -783,6 +783,7 @@ asmlinkage long sys_adjtimex_time32(struct old_timex32 __user *txc_p);

 /* kernel/sys.c */
 asmlinkage long sys_getpid(void);
+asmlinkage long sys_chippy(void);
 asmlinkage long sys_getppid(void);
 asmlinkage long sys_getuid(void);
 asmlinkage long sys_geteuid(void);
diff --git a/include/uapi/asm-generic/unistd.h b/include/uapi/asm-generic/unistd.h
index 45fa180cc56a..fe7209caf314 100644
--- a/include/uapi/asm-generic/unistd.h
+++ b/include/uapi/asm-generic/unistd.h
@@ -520,6 +520,8 @@ __SC_3264(__NR_adjtimex, sys_adjtimex_time32, sys_adjtimex)
 /* kernel/sys.c */
 #define __NR_getpid 172
 __SYSCALL(__NR_getpid, sys_getpid)
+#define __NR_chippy 400
+__SYSCALL(__NR_chippy, sys_chippy)
 #define __NR_getppid 173
 __SYSCALL(__NR_getppid, sys_getppid)
 #define __NR_getuid 174
diff --git a/kernel/sys.c b/kernel/sys.c
index 339fee3eff6a..0474a8676476 100644
--- a/kernel/sys.c
+++ b/kernel/sys.c
@@ -954,6 +954,12 @@ SYSCALL_DEFINE0(getpid)
        return task_tgid_vnr(current);
 }

+SYSCALL_DEFINE0(chippy)
+{
+       printk("chippy !!\r\n");
+       return task_tgid_vnr(current);
+}
+
 /* Thread ID - the internal kernel "pid" */
 SYSCALL_DEFINE0(gettid)
 {
```



## 000

strace 工具可根据程序的名称输出系统调用的过程

ltrace工具显示出了程序在用户空间的调用


启动方式

