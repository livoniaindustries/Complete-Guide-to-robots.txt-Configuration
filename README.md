# Complete Guide to robots.txt Configuration

**🤖 What is robots.txt?** robots.txt is a service file located in the root directory of a website. It contains directives that instruct search engine bots which URLs should be crawled and indexed, and which should be ignored. It's essentially a set of recommendations for search robots, not a strict access control mechanism.

**⚠️ Important:** robots.txt is just a set of guidelines. Search engines may still index pages if other sites link to them. This file is not intended to prevent unauthorized access to sensitive content—use proper authentication for that.

## Key Features of robots.txt

*   **Remove duplicates:** Prevent indexing of duplicate content and similar pages
*   **Hide technical pages:** Block search engines from indexing admin areas, scripts, or temporary files
*   **Exclude error pages:** Prevent 404 pages and error messages from appearing in search results
*   **Control pagination:** Manage how paginated content is indexed
*   **Block resources:** Prevent crawling of CSS, JavaScript, or image files (though this may affect how search engines render pages)
*   **Selective blocking:** Hide your site from specific search engines while allowing others

## Rules for Using robots.txt

| Rule | Description |
| --- | --- |
| File format | Plain text in UTF-8 encoding |
| File location | Must be in the root directory of your site (e.g., https://example.com/robots.txt) |
| Uniqueness | Only one robots.txt file per site |
| Record structure | All records should start with User-agent (defining which bot the rules apply to) |
| Required directives | Each rule must include either Allow: or Disallow: directives |
| Command limit | Maximum 1024 commands per file |
| File size | Should ideally be under 500 KB |

## Directives and Special Characters

### Main Directives

| Directive | Description | Example |
| --- | --- | --- |
| User-agent: | Specifies which search robot the following rules apply to | `User-agent: Googlebot` |
| Disallow: | Indicates which directories or pages cannot be crawled | `Disallow: /admin/` |
| Allow: | Indicates which directories or pages can be crawled (useful for overriding Disallow for specific paths) | `Allow: /blog/public` |
| Sitemap: | Points to the location of your XML sitemap | `Sitemap: https://example.com/sitemap.xml` |
| Clean-param: | Used when URL contains GET parameters (not binding, mainly for Yandex) | `Clean-param: utm_source /catalog` |
| Crawl-delay: | Specifies delay between crawls in seconds (not supported by all search engines) | `Crawl-delay: 10` |
| Host: | Specifies the main mirror of the site (Yandex-specific, now deprecated) | `Host: https://example.com` |

### Special Characters

#

Start of comment

/

Path separator, placed after directive, before directory or file name

\*

Wildcard - matches any sequence of characters (supported by most search engines)

$

End of URL pattern - URLs ending with this pattern become available for indexing

## Basic robots.txt Examples

### 1\. Allow Full Access to All Bots

```
User-agent: *
Allow: /
```

### 2\. Block All Bots (Full Site)

```
User-agent: *
Disallow: /
```

### 3\. Block Specific Directories

```
User-agent: *
Disallow: /cgi-bin/
Disallow: /tmp/
Disallow: /private/
Disallow: /admin/
```

### 4\. Block Specific File Types

```
User-agent: *
Disallow: /*.pdf$
Disallow: /*.zip$
Disallow: /*.mp3$
```

### 5\. Block Specific Search Engines

```
# Block all Yandex bots
User-agent: Yandex
Disallow: /

# Block all Google bots
User-agent: Googlebot
Disallow: /

# Allow all other bots
User-agent: *
Allow: /
```

## Advanced robots.txt Examples

### 6\. Block Everything Except Specific Path

```
User-agent: *
Disallow: /
Allow: /public/
Allow: /blog$
```

### 7\. Block All Pages Starting with /blog Except /blog/public

```
User-agent: *
Allow: /blog/public
Disallow: /blog
```

### 8\. Block All Pages with Query Parameters

```
User-agent: *
Disallow: /*?*
Allow: /?page=1$
```

### 9\. Block Specific File with Allow Override

```
User-agent: *
Allow: /css/
Allow: /images/logo.png
Disallow: /images/
```

### 10\. Using Clean-param for GET Parameters

```
User-agent: *
Disallow:
Clean-param: utm_source /
Clean-param: get /folder/page.php
Clean-param: ref /catalog
```

## Search Engine User-Agent Names

| Search Engine | User-Agent |
| --- | --- |
| Google | Googlebot |
| Google Images | Googlebot-Image |
| Google Mobile | Googlebot-Mobile |
| Google News | Googlebot-News |
| Google Video | Googlebot-Video |
| Yandex | YandexBot |
| Yandex Images | YandexImages |
| Bing | bingbot |
| Baidu | Baiduspider |
| DuckDuckGo | DuckDuckBot |
| Facebook | facebookexternalhit |
| Twitter | Twitterbot |
| Apple | Applebot |
| Slurp (Yahoo) | Slurp |

## CMS-Specific robots.txt Examples

### WordPress

```
User-agent: *
Disallow: /wp-admin/
Disallow: /wp-includes/
Disallow: /wp-content/plugins/
Disallow: /wp-content/cache/
Disallow: /wp-content/themes/
Disallow: /xmlrpc.php
Disallow: /wp-login.php
Disallow: /readme.html
Allow: /wp-content/uploads/

Sitemap: https://example.com/sitemap.xml
```

### Joomla

```
User-agent: *
Disallow: /administrator/
Disallow: /bin/
Disallow: /cache/
Disallow: /cli/
Disallow: /components/
Disallow: /includes/
Disallow: /installation/
Disallow: /language/
Disallow: /layouts/
Disallow: /libraries/
Disallow: /logs/
Disallow: /modules/
Disallow: /plugins/
Disallow: /tmp/
```

### Drupal

```
User-agent: *
Disallow: /core/
Disallow: /profiles/
Disallow: /vendor/
Disallow: /modules/
Disallow: /themes/
Disallow: /sites/
Disallow: /CHANGELOG.txt
Disallow: /cron.php
Disallow: /install.php
Disallow: /README.txt
Disallow: /update.php
Disallow: /web.config
```

### Magento

```
User-agent: *
Disallow: /index.php/
Disallow: /catalog/product_compare/
Disallow: /catalog/category/view/
Disallow: /catalog/product/view/
Disallow: /checkout/
Disallow: /customer/
Disallow: /wishlist/
Disallow: /review/
Disallow: /tag/
```

## Sitemap Integration

**📌 Sitemap Directive:** You can specify the location of your XML sitemap in robots.txt to help search engines discover all your important pages.

```
Sitemap: https://example.com/sitemap.xml
Sitemap: https://example.com/sitemap-index.xml
Sitemap: https://example.com/sitemap-images.xml
```

## Common Use Cases with Examples

### Prevent Duplicate Content

```
User-agent: *
Disallow: /*?sort=
Disallow: /*?page=
Disallow: /*print=true
Disallow: /*utm_source=
Disallow: /*utm_medium=
Disallow: /*utm_campaign=
```

### Block Pagination Pages

```
User-agent: *
Disallow: /page/
Disallow: /category/*/page/
Disallow: /*/page/[0-9]+$
```

### Block Search Results Pages

```
User-agent: *
Disallow: /search
Disallow: /search/
Disallow: /?s=
Disallow: /?q=
```

### Block Temporary and Staging Sites

```
# Block all bots on staging site
User-agent: *
Disallow: /
```

### Different Rules for Different Bots

```
# Google - block images
User-agent: Googlebot-Image
Disallow: /

# Google - allow everything else
User-agent: Googlebot
Allow: /

# Yandex - block everything
User-agent: Yandex
Disallow: /

# Bing - block specific directories
User-agent: bingbot
Disallow: /private/
Disallow: /temp/

# All other bots - allow everything
User-agent: *
Allow: /
```

## Testing Your robots.txt

**🔍 How to test:** Most search engines provide tools to test your robots.txt file:

*   **Google:** Search Console → robots.txt Tester
*   **Yandex:** Webmaster → Tools → robots.txt analysis
*   **Bing:** Webmaster Tools → robots.txt tester

### View Your robots.txt

```
https://yourdomain.com/robots.txt
```

### Check robots.txt with cURL

```
curl https://example.com/robots.txt
```

## Common Mistakes to Avoid

| Mistake | Why It's Bad | Correct Approach |
| --- | --- | --- |
| Blocking CSS/JS files | Search engines may not render pages correctly | Allow CSS/JS, use meta tags for sensitive content |
| Using robots.txt for sensitive data | robots.txt is public - anyone can see what you're hiding | Use password protection or authentication |
| Missing trailing slashes | `Disallow: /admin` blocks both /admin and /admin123 | Use `Disallow: /admin/` for exact directory |
| Blocking all bots unintentionally | Site disappears from search results | Double-check Disallow: / rules |
| Using incorrect user-agent names | Rules don't apply to intended bots | Check official names for each search engine |

## Complete robots.txt Templates

### Template 1: Standard Website

```
# Allow all bots full access
User-agent: *
Allow: /

# Sitemap location
Sitemap: https://example.com/sitemap.xml
```

### Template 2: E-commerce Site

```
User-agent: *
Allow: /
Disallow: /checkout/
Disallow: /cart/
Disallow: /my-account/
Disallow: /*?sort=
Disallow: /*?order=
Disallow: /*?limit=
Disallow: /search/
Allow: /product/
Allow: /category/

Sitemap: https://example.com/sitemap.xml
```

### Template 3: Blog/News Site

```
User-agent: *
Allow: /
Disallow: /wp-admin/
Disallow: /wp-includes/
Disallow: /tag/
Disallow: /author/
Disallow: /page/
Allow: /category/
Allow: /*/page/1$

Sitemap: https://example.com/sitemap.xml
```

### Template 4: Development/Staging Site

```
# Block all search engines
User-agent: *
Disallow: /

# Prevent indexing completely
User-agent: Googlebot
Disallow: /

User-agent: Yandex
Disallow: /

User-agent: bingbot
Disallow: /
```

## Quick Reference

| Directive | Example | Effect |
| --- | --- | --- |
| Allow all | `Allow: /` | Entire site can be crawled |
| Block all | `Disallow: /` | Nothing can be crawled |
| Block directory | `Disallow: /private/` | /private/ directory blocked |
| Block file type | `Disallow: /*.pdf$` | All PDF files blocked |
| Block with wildcard | `Disallow: /*?sort=*` | URLs with sort parameter blocked |
| Allow specific file | `Allow: /public/report.pdf` | Only this PDF is allowed |
| Specific bot only | `User-agent: Googlebot` | Rules only for Google |
| Sitemap | `Sitemap: /sitemap.xml` | Points to sitemap location |

## Resources and Validation Tools

*   **Google robots.txt Tester:** Available in Google Search Console
*   **Yandex Webmaster:** robots.txt analysis tool
*   **Bing Webmaster Tools:** robots.txt validation
*   **Online validators:** https://en.ryte.com/free-tools/robots-txt/
*   **Official documentation:** https://developers.google.com/search/docs/crawling-indexing/robots/intro

**⚠️ Remember:** robots.txt is publicly accessible. Anyone can view your robots.txt file at yourdomain.com/robots.txt. Never use it to hide sensitive information—use proper server-side authentication instead.
