`该文章转载于 http://bqzzd.cn/402.html`

图片放大功能其实可以用插件做到，比如 `Easy FancyBox` `FancyBox for WordPress` 这些插件安装好以后只要在文章内插入图片，然后就行了。但是因为我平时都是使用 Markdown 语法写作插入图片。MD 语法经过 WordPress 解释器转成 Html 如下： `<img title="name" alt="name" src="url">` 但是这些插件要求的样式如下： `<a href=""><img src="url"></a>` 所以明显不适用，要将如上格式改成如下。不可能一张张手动修改，太累。

安装点击图片放大框架 这里并没有选择如上两个插件，使用网上 github 开源的一个框架。点击下载框架

解压到 WP 主题所在文件夹

/wp-content/themes/主题名/fancybox header.php添加代码，放在之前

```markup
<link href="<?php bloginfo('template_url'); ?>/fancybox/source/jquery.fancybox.css?v=2.1.5" rel="stylesheet" media="all" />
```

注意位置，是而不是

footer.php中添加代码，放在之前

```markup
<script type="text/javascript" src="<?php bloginfo('template_url'); ?>/fancybox/lib/jquery-1.10.1.min.js"></script>
<script type="text/javascript" src="<?php bloginfo('template_url'); ?>/fancybox/source/jquery.fancybox.pack.js?v=2.1.5"></script>
<script>
    // 给图片添加链接
    $(document).ready(function() {
        $("p img").each(function() {
        var strA = "<a id='yourid' href='" + this.src + "'></a>";
        $(this).wrapAll(strA);
        });
    });
    // fancybox
    $("#yourid").fancybox({
        openEffect    : 'elastic',
        closeEffect   : 'elastic',
    });
</script>
```

ok 到这里就没问题，亲测可行。
