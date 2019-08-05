---
layout: post
title: Docker Compose Demo
category: demo
tags: [demo]
excerpt: Docker Compose Demo !
keywords: demo
---

---

# 目录树

## 参考资料
https://blog.51cto.com/9291927/2310444

## Demo Project
### 2.1
### 2.2

- 源代码
```
@Data
@NoArgsConstructor
@AllArgsConstructor
public class ResultEntity<T> {
    private String code;
    private String msg;
    private T data;

    public static <T> ResultEntity<T> getSuccessResult(T data) {
        return new ResultEntity<T>(MessageConstant.CODE_SUCCESS, MessageConstant.MESSAGE_SUCCESS, data);
    }

    public static <T> ResultEntity<T> getSuccessResult() {
        return new ResultEntity<T>(MessageConstant.CODE_SUCCESS, MessageConstant.MESSAGE_SUCCESS, null);
    }

    public static <T> ResultEntity<T> getResult(String code, String message) {
        return new ResultEntity<T>(code, message, null);
    }

}
```