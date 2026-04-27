# Week 9：Flask (Flask)
[首页](00：目录 (Table of Contents).md)

## 目录
* [[#Flask 框架 (Flask Framework)]]
* [[#布局与模板 (Layouts and Templates)]]
* [[#GET 与 POST (GET vs. POST)]]
* [[#会话与 Cookie (Sessions and Cookies)]]
* [[#AJAX 与 JSON (AJAX and JSON)]]

## Flask 框架 (Flask Framework)

*   用于构建动态 Web 应用程序的 Python “微框架”。
*   **结构：** `app.py` 处理逻辑，`templates/` 文件夹存放 HTML。
*   **Jinja2：** HTML 中的占位符语法，如 `{{ name }}`。

## 布局与模板 (Layouts and Templates)

*   `layout.html` 定义公共结构。
*   其他页面使用 `{% extends "layout.html" %}` 和 `{% block body %}` 来“扩展”布局，避免重复。

## GET 与 POST (GET vs. POST)

*   **GET：** 数据在 URL 中可见（用于搜索）。
*   **POST：** 数据在请求体中隐藏（用于处理敏感数据）。

## 会话与 Cookie (Sessions and Cookies)

*   **Cookie：** 存储在用户计算机上的小文件，用于向服务器标识用户。
*   **会话 (Sessions)：** 允许服务器“记住”用户（例如保持登录状态）。

## AJAX 与 JSON (AJAX and JSON)

*   **API：** 与其他服务交互的规范。
*   **AJAX：** 允许网页在后台异步更新，无需重新加载整个页面。
*   **JSON：** 键值对形式的数据格式，常用于服务器与 Web 应用间的数据传输。
