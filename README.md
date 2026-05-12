# SBA 综合安全运维引擎 (v4.1.0) 🛡️

[简体中文](#-简体中文) | [English](#-english)

---

## 🇨🇳 简体中文

**SBA (Site Behavior Auditor)** 是一款专为 WordPress 深度定制的高性能、全链路安全加固与审计套件。通过物理级入口封锁与工业级异步统计架构，SBA 能在不牺牲服务器性能的前提下，为您的网站建立起一道坚固的防御屏障。

### 💎 核心功能模块

#### 1. 🚫 入口物理封锁 (Entrance Sequestration)
*   **登录墙**：直接物理拦截未授权用户对 `wp-login.php` 和 `wp-admin` 目录的访问。这种拦截发生在加载主题之前，能有效节省 CPU 资源并终结暴力破解。
*   **侧边栏极简登录**：不再建议创建繁琐的私密登录页。通过将 `[sba_login_box]` 短代码放置在网站的**侧边栏小工具（自定义 HTML/文本）**中，访客即可在前台通过 iOS 风格面板完成登录、注册或找回密码，且完全兼容全站静态缓存。

#### 2. 📊 高性能行为审计 (Behavioral Auditing)
*   **写缓冲架构 (Write-Back)**：借鉴存储设备的写缓存逻辑，PV 统计先进入内存缓冲，定期批量写回数据库，将高并发下的磁盘 I/O 写入压力降低 99% 以上。
*   **Cloudflare 官方节点感知**：内置 CF 全球官方 IP 段。针对 CF 扫描 IP 自动开启“只审计不拦截”模式，确保云端健康检查能正常穿透，同时在轨迹中留下详细的审计证据。
*   **今日日志一键导出**：拦截列表支持一键导出今日数据为 CSV 文件。针对 Excel 优化了 UTF-8 BOM 编码，确保在 Windows 环境下打开无乱码。

#### 3. 🛡️ 深度 WAF 防御 (System Hardening)
*   **隐藏蜜罐 (Honeypot)**：自动在页面投放仅爬虫可见的隐藏链接，精准诱捕并封禁恶意采集器。
*   **SSRF 深度防护**：监控站内发起的出站请求，防止内网探测。智能放行 WP-Cron 回环请求，确保定时任务不受干扰。
*   **指纹抹除**：自动抹除 WordPress 版本号、脚本 `ver` 参数及 `X-Powered-By` 头，实现全站“深度隐身”。

### ⚙️ 环境要求
*   **PHP 版本**：7.4 或 8.x（强烈建议开启 **Zend OpCache** 以获得极致性能）。
*   **WordPress**：6.0 及以上版本。
*   **必要权限**：对 `wp-content/uploads` 目录的写入权限。

### 🚀 部署指南
1.  **面板部署**：进入「外观」->「小工具」，添加一个“自定义 HTML”到侧边栏，填入短代码 `[sba_login_box]`。
2.  **IP 数据**：在设置页面底部上传 `ip2region_v4.xdb`（IPv4 库）和 `ip2region_v6.xdb`（可选）。
3.  **环境配置**：若使用 Cloudflare，请在「IP 信任来源」中选择 `Cloudflare (CF_IP)`。
4.  **统计增强**：若网站使用了静态缓存，请开启「AJAX 统计补丁」。

---

## 🇺🇸 English

**SBA (Site Behavior Auditor)** is a professional-grade security infrastructure and auditing suite for WordPress. It combines high-performance traffic monitoring with a "Zero-Attack-Surface" strategy to protect your site from modern web threats and automated scans.

### ✨ Key Features

#### 1. 🔒 Physical Entrance Lockdown
*   **Admin Sequestration**: Physically blocks direct access to `wp-login.php` and `wp-admin` for unauthenticated visitors, stopping brute-force attacks at the earliest stage.
*   **Sidebar Authentication**: We recommend placing the **[sba_login_box]** shortcode in your **Sidebar/Widget** area. It renders a sleek, iOS-style AJAX panel that supports login, registration, and recovery, fully compatible with full-page caching.

#### 2. 📈 High-Performance Auditing
*   **Write-Back Architecture**: Inspired by enterprise storage systems, statistics are buffered in memory and flushed to the database in intervals, reducing DB write load by over **99%**.
*   **Cloudflare Infrastructure Awareness**: Pre-configured with official Cloudflare IP ranges. It automatically switches official CF scans to "Audit-only" mode—tracking their movement without blocking, ensuring seamless CDN health checks.
*   **One-Click Log Export**: Easily download today's blocked logs as a CSV file. Includes a **UTF-8 BOM** fix for perfect compatibility with Microsoft Excel.

#### 3. 🛡️ System Hardening & WAF
*   **Silent Honeypot**: Deploys hidden decoy links to catch and ban malicious scrapers.
*   **SSRF Protection**: Filters outbound requests to prevent internal network probing while intelligently bypassing loopback requests for **WP-Cron**.
*   **Fingerprint Erasing**: Removes sensitive version info and headers to make your site "invisible" to automated fingerprinting tools.

### 📋 Technical Requirements
*   **PHP**: 7.4 or 8.x (**Zend OpCache** highly recommended for peak efficiency).
*   **WordPress**: 6.0 or higher.
*   **Permissions**: Write access to `wp-content/uploads` for auditing database management.

### 🛠️ Getting Started
1.  **Deploy Portal**: Add a "Custom HTML" widget to your sidebar and insert the shortcode `[sba_login_box]`.
2.  **IP Database**: Upload the `ip2region_v4.xdb` file via the settings page to enable accurate geo-location.
3.  **Trust Source**: If using a CDN like Cloudflare, select the correct IP source (e.g., `HTTP_CF_CONNECTING_IP`) in settings.
4.  **Cache Patching**: Enable the **"AJAX Statistics Patch"** if your site uses full-page caching.

---

### 🖼️ 界面预览 (Screenshots)

#### 可视化审计面板 (Audit Dashboard)
<p align="left">
  <img src="https://github.com/user-attachments/assets/bea56093-224b-4124-aa43-a15a06032091" alt="Audit Dashboard" width="70%">
</p>

#### 实时轨迹与拦截日志 (Real-time Trace & Logs)
<p align="left">
  <img src="https://github.com/user-attachments/assets/1a323212-bdf8-46ae-b079-9563f80a4eac" alt="Trace" width="45%">
  <img src="https://github.com/user-attachments/assets/d1595991-1dde-455e-91b7-4eccbf805230" alt="Blocked Logs" width="45%">
</p>

#### 防御设置与环境检测 (Settings & Env Check)
<p align="left">
  <img src="https://github.com/user-attachments/assets/4b1daf8e-3223-41eb-bbde-9cce9f390a80" alt="Settings" width="70%">
</p>

#### iOS 风格登录交互 (iOS Style Login)
<p align="left">
  <img src="https://github.com/user-attachments/assets/1be6cceb-887d-4b44-97b5-304a69e3ba04" width="130">
  <img src="https://github.com/user-attachments/assets/9de3d9ed-8f44-4c4a-9080-1b6133ddf884" width="130">
  <img src="https://github.com/user-attachments/assets/c28151e0-fd64-43a7-bc18-40463c9b4fa1" width="130">
</p>

#### SMTP 邮件设置 (SMTP Mail Settings)
<p align="left">
  <img src="https://github.com/user-attachments/assets/4550941c-f32f-4626-98ec-c7d6a3ed7620" alt="SMTP Settings" width="70%">
</p>

---

### 🤝 Acknowledgments
High-performance IP resolution is powered by [ip2region](https://github.com/lionsoul2014/ip2region).

---

## 📄 License
GPL v2 or later

---
**Developed by Stone** | *Architect-grade stability for the WordPress ecosystem.*