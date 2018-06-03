# REST APIを作成する

次に、著者名を指定して書籍情報を取得するREST APIを作成します。

## リポジトリーインターフェースの修正

まず、リポジトリーに著者名で検索するメソッドを追加します。
Spring Dataでは、メソッド名からクエリを自動生成してくれるため、
インターフェースへのメソッド定義の追加のみを行います。

1. BookInfoRepositoryインターフェースを以下の通り修正する。
    
    ```
    package com.example.demo.repository;
    
    import com.example.demo.model.BookInfo;
    import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
    import org.springframework.stereotype.Repository;
    
    import java.util.List;
    
    @Repository
    public interface BookInfoRepository extends DocumentDbRepository<BookInfo, String> {
        List<BookInfo> findByAuthor(String author);
    }
    ```
    
    ※もともと、メソッドが1つも定義されていなかったところに、findByAuthorメソッドを追加した。

## API用コントローラークラスの作成

1. 「com.example.demo」の下に「api」パッケージを作成する。
1. 「api」パッケージの下に「BookListApiController」クラスを作成する。
1. 「BookListApiController」クラスを以下の通り修正する。
    
    ```
    package com.example.demo.api;
    
    import com.example.demo.model.BookInfo;
    import com.example.demo.repository.BookInfoRepository;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestParam;
    import org.springframework.web.bind.annotation.RestController;
    
    import java.util.ArrayList;
    import java.util.List;
    
    @RestController
    @RequestMapping("api")
    public class BookListApiController {
        
        @Autowired
        private BookInfoRepository repository;
        
        @GetMapping
        public List<BookInfo> getAllBookInfo(@RequestParam("author") String author) {
            List<BookInfo> bookList = new ArrayList<>();
            repository.findByAuthor(author).forEach(b -> bookList.add(b));
            
            return bookList;
        }
        
    }
    ```

1. IntelliJ IDEAでDemoApplication.main()を実行し、アプリケーションを開始する。
1. アプリケーションが起動される（ログに「Started DemoApplication in x.xxx seconds」が表示される）まで待つ。
1. 「スタート＞Git＞Git Bash」を選び、Git Bashを起動する。
1. Git Bashで以下のコマンドを実行する。
    
    ```
    $ curl 'http://localhost:8080/api?author=%E6%A3%AE%E9%B4%8E%E5%A4%96'
    ```
    
    ※URLエンコードされた文字列「%E6%A3%AE%E9%B4%8E%E5%A4%96」は「森鴎外」のUTF-8表現に対応するもの。

1. 以下の通り、該当するデータのJSONが返却されることを確認する。
    
    ```
    [{"id":"2","title":"山椒大夫・高瀬舟","author":"森鴎外","publisher":"新潮社","price":529}]
    ```

1. 問題なく表示されたら、アプリケーションを終了する。
