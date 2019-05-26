- 路由
  - /test/getId
```

<?php declare(strict_types=1);

/**
 * Class TestController
 * @Controller()
 */
class TestController
{
    /**
     * @RequestMapping()
     * @return string
     */
    public function getId()
    {
        return "get id";
    }
}

```
