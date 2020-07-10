---
title: 文章
media_order: walle.jpg
hide_git_sync_repo_link: false
routable: true
cache_enable: true
visible: true
hero_image: walle.jpg
blog_url: /blog
show_sidebar: false
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
    enabled: false
post_icon: newspaper-o
feed:
    limit: 10
---

<font size="3" color="white">用数学的理论去解释程序的运行，用程序的运行去验证数学的理论！</font>