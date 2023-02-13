# photo
Wordpress图床仓库
#WordPress数据库搬家
<!-- wp:heading -->
<h2 id="toc_6"><strong>更换空间，也更换域名</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>但有时，我们也可能会碰到更换域名的情况，比如测试环境迁移到正式环境，或者要使用现有数据搭建一个新的站点的情况，这时，我们就需要进行新旧域名的替换操作，来实现新域名站点的正常访问，这种情况其实也不难，在执行好上面搬家的操作之后，再去执行2个简单的数据库语句就可以完成相应的新旧域名替换了。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3 id="toc_7"><strong>1. 更改WordPress设置选项内的旧域名</strong></h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>首先用phpmyadmin打开你的数据库（或者在你的主机管理里找到对应的数据库管理，这里不推荐使用第三方数据库管理软件），然后找到并打开 wp_options 这个数据表（wp_为表前缀），切换到SQL状态，在输入栏中输入如下代码执行即可：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>UPDATE wp_options SET option_value = replace( option_value, '老域名', '新域名');</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>通过以上SQL执行语句来完成自定义设置选项中涉及到的旧域名更改，只有这一步操作执行完毕后，才可以顺利进入后台，否则即使你输入密码，也会自动跳转到原来的老域名站点。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3 id="toc_8"><strong>2. 更改文章（页面）中涉及的旧域名</strong></h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>在我们执行过第1步后，已经可以正常进入网站后台进行管理了，但在访问文章（页面）内容时，会发现文章（页面）中的图片还是没法显示，那么，我们就需要执行下面的操作了。进入 phpmyadmin 数据库管理（或者在你的主机管理里找到对应的数据库管理），找到 wp_posts 这个数据表（wp_为表前缀），切换到SQL状态，在输入栏中输入如下代码执行即可：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>UPDATE wp_posts SET post_content = replace( post_content, '老域名','新域名') ;</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>执行该操作后，文章（页面）中的图片也就可以正常显示了。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3 id="toc_9"><strong>3. 更改文章（页面）的自定义栏目中涉及的旧域名</strong></h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>修改文章（页面）中自定义栏目中涉及的旧域名，比如产品图片的自定义栏目，可能会涉及到域名地址，那么，我们就只需要执行下面的操作就可以。进入 phpmyadmin 数据库管理（或者在你的主机管理里找到对应的数据库管理），找到 wp_postmeta 这个数据表（wp_为表前缀），切换到SQL状态，在输入栏中输入如下代码执行即可：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>UPDATE wp_postmeta SET meta_value = replace(meta_value, '老域名','新域名') ;</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>执行该操作后，文章（页面）中的图片也就可以正常显示了。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>备注：</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>执行的SQL操作语句中，其中的 wp_ 是你的网站数据库的前缀（如果你在安装WordPress自定义过数据库前缀，请先修改为自己的）。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>例如：以上老域名格式为：http://www.baidu.com；新域名格式为 http://www.360.com</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>经过以上数据库操作，就可以把以前老网站的老域名全部更改替换为新站点的域名，等待解析生效后，更换域名后的网站就可以使用新域名正常访问了。</p>
<!-- /wp:paragraph -->
