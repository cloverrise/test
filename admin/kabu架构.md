```mermaid

flowchart TB

%% =====================================
%% 投资学习平台系统架构图
%% =====================================

%% 用户访问层
subgraph ACCESS["用户访问层"]

    U1[普通用户<br/>会员]

    U2[管理员]

end

%% 前端访问
U1 --> WEBENTRY[访问前端网站<br/>Web]

%% 后台访问
U2 --> ADMINENTRY[访问后台管理系统<br/>Admin]

%% =====================================
%% 前台系统
%% =====================================

subgraph WEB["前台系统（用户访问）"]

     direction LR
    W1[会员中心] ~~~ W2[在线预约] ~~~ W5[支付系统]
    
    W4[问卷系统] ~~~ W3[学习系统] ~~~ W6[聊天系统]
end

%% =====================================
%% 后台系统
%% =====================================

subgraph ADMIN["后台管理系统（管理员访问）"]

    direction LR
    A1[顾客管理] ~~~ A2[预约管理] ~~~ A3[广告管理] ~~~ A4[邮件管理] ~~~ A5[学习管理]
    %% 第二行
    A6[入金管理] ~~~ A7[聊天管理] ~~~ A8[问卷管理] ~~~ A10[权限管理] ~~~ A11[日志管理]  

end

%% =====================================
%% 应用服务层
%% =====================================

subgraph APP["业务服务层"]

    direction TB

    APP1[用户认证服务]

    APP2[支付服务]

    APP3[问卷服务]

    APP4[邮件服务]

    APP5[统计分析服务]

end


%% =====================================
%% 数据存储层
%% =====================================

subgraph DB["数据存储层"]

    direction LR

    D1[(MySQL<br/>Redis)]

    CACHE[(Redis)]

end

%% =====================================
%% 第三方服务
%% =====================================

subgraph API["第三方服务"]

    direction TB

    T2[支付接口]

    T3[SMTP邮件系统]

end

%% =====================================
%% 系统流程
%% =====================================

WEBENTRY --> WEB

ADMINENTRY --> ADMIN

WEB --> APP

ADMIN --> APP

APP --> API

APP --> DB

%% =====================================
%% 样式
%% =====================================

classDef user fill:#FFF7E6,stroke:#4A90E2,stroke-width:1px,color:#000;
classDef web fill:#EEF5FF,stroke:#4A90E2,stroke-width:1px,color:#000;
classDef admin fill:#F3FFF3,stroke:#2E8B57,stroke-width:1px,color:#000;
classDef app fill:#F8F3FF,stroke:#7A4DCC,stroke-width:1px,color:#000;
classDef db fill:#FFF0F0,stroke:#D9534F,stroke-width:1px,color:#000;
classDef api fill:#F3E5F5,stroke:#9C27B0,stroke-width:1px,color:#000;

class ACCESS user;

class WEB web;

class ADMIN admin;

class APP app;

class DB db;

class API api;
