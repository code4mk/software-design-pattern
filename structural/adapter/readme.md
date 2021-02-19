# Adapter design pattern

* convert one to another.

```php
class SampleBook
{
    private $author;
    private $title;
    public function __construct($author,$title)
    {
        $this->author = $author;
        $this->title = $title;
    }

    public function getAuthor()
    {
        return $this->author;
    }

    public function getTitle()
    {
        return $this->title;
    }
}

class BookAdapter
{
    private $book;

    public function __construct(SampleBook $book)
    {
        $this->book = $book;
    }

    public function getAuthorTitle()
    {
        return $this->book->getAuthor() . ' -- '. $this->book->getTitle();
    }
}

$book = new SampleBook('kamal',' easy design pattern');
$bookAdapter =  new BookAdapter($book);

print_r($bookAdapter->getAuthorTitle());
```

# resource

* https://www.geeksforgeeks.org/adapter-pattern/
