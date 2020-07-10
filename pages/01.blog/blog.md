---
title: 首页
media_order: walle.jpg
hide_git_sync_repo_link: false
routable: true
cache_enable: true
visible: true
hero_image: walle.jpg
blog_url: /blog
show_sidebar: true
show_breadcrumbs: false
show_pagination: true
content:
    items:
        - '@self.children'
    limit: 5
    order:
        by: date
        dir: desc
    pagination: true
    url_taxonomy_filters: true
bricklayer_layout: true
display_post_summary:
    enabled: true
post_icon: file-text
feed:
    limit: 10
---

<font size="8" face="arial" color="white">用数学去解释程序，用程序去验证数学！</font>