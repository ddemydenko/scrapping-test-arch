## Pattern Management

### Basic Pattern Components

1. **HTML Structure Example**
```html
<article class="news-item">
    <h2 class="title">Заголовок новини</h2>
    <div class="content">Текст новини</div>
    <span class="date">2024-12-12</span>
</article>
```


### Pattern Types

1. **Simple Selectors**
```json
{
    "title": {
        "selector": ".news-item .title",
        "required": true,
        "type": "text"
    },
    "content": {
        "selector": ".news-item .content",
        "required": true,
        "type": "html"
    }
}
```

2. **Navigation Rules**
```json
{
    "pagination": {
        "nextButton": ".pagination .next",
        "maxPages": 5
    },
    "articleLinks": {
        "selector": ".article-list .article-link",
        "attribute": "href",
        "pattern": "^/news/\\d+"
    }
}
``` 

### Pattern Storage Example

```json
{
    "patternId": "news-site-001",
    "version": "1.2.0",
    "lastUpdated": "2024-12-13T10:00:00Z",
    "selectors": {
        "title": {
            "selector": ".news-item .title",
            "required": true,
            "minLength": 10
        },
        "content": {
            "selector": ".news-item .content",
            "required": true,
            "minLength": 100
        },
        "date": {
            "selector": ".news-item .date",
            "transform": "parseDate('DD-MM-YYYY')"
        }
    },
    "navigation": {
        "pagination": {
            "nextButton": ".pagination .next",
            "maxPages": 5
        }
    },
    "validation": {
        "title": {
            "minLength": 10,
            "maxLength": 200
        },
        "content": {
            "minLength": 100,
            "required": true
        }
    }
}
```

### Pattern Update Workflow

1. **Detection of Changes**
    - Monitoring system detects site structure changes
    - Failed scraping attempts trigger alerts
    - Admin reviews the changes

2. **Pattern Updates**
    - Admin updates patterns through interface
    - System validates new patterns
    - Changes are versioned and stored

3. **Deployment**
    - New patterns are immediately available
    - No system restart required
    - Automatic fallback if issues detected
