# POSIX

###  サマリ

> **POSIX**（ポシックス、ポジックス、[英](https://ja.wikipedia.org/wiki/%E8%8B%B1%E8%AA%9E): Portable operating system interface）は、各種[UNIX](https://ja.wikipedia.org/wiki/UNIX)を始めとする異なる[オペレーティングシステム](https://ja.wikipedia.org/wiki/%E3%82%AA%E3%83%9A%E3%83%AC%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0) \(OS\) 実装に共通の[アプリケーションプログラミングインタフェース](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%95%E3%82%A7%E3%83%BC%E3%82%B9) \(API\) を定め、移植性の高い[アプリケーションソフトウェア](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%BD%E3%83%95%E3%83%88%E3%82%A6%E3%82%A7%E3%82%A2)の開発を容易にすることを目的として[IEEE](https://ja.wikipedia.org/wiki/IEEE)が策定したAPI規格である。POSIXという名前は[リチャード・ストールマン](https://ja.wikipedia.org/wiki/%E3%83%AA%E3%83%81%E3%83%A3%E3%83%BC%E3%83%89%E3%83%BB%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%83%9E%E3%83%B3)がIEEEに提案したものである[\[1\]](https://ja.wikipedia.org/wiki/POSIX#cite_note-faq-1)。末尾の「X」はUNIX互換OSに「X」の字がつく名前が多いことからつけられた。[ISO/IEC JTC 1/SC 22](https://ja.wikipedia.org/wiki/ISO/IEC_JTC_1/SC_22)でISO/IEC 9945として国際規格になっている。

### 仕様

> 規格の内容は[カーネル](https://ja.wikipedia.org/wiki/%E3%82%AB%E3%83%BC%E3%83%8D%E3%83%AB)への[C言語](https://ja.wikipedia.org/wiki/C%E8%A8%80%E8%AA%9E)の[インタフェース](https://ja.wikipedia.org/wiki/%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%95%E3%82%A7%E3%83%BC%E3%82%B9_%28%E6%83%85%E5%A0%B1%E6%8A%80%E8%A1%93%29)である[システムコール](https://ja.wikipedia.org/wiki/%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%82%B3%E3%83%BC%E3%83%AB)に留まらず、[プロセス](https://ja.wikipedia.org/wiki/%E3%83%97%E3%83%AD%E3%82%BB%E3%82%B9)環境、[ファイル](https://ja.wikipedia.org/wiki/%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB_%28%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF%29)と[ディレクトリ](https://ja.wikipedia.org/wiki/%E3%83%87%E3%82%A3%E3%83%AC%E3%82%AF%E3%83%88%E3%83%AA)、システムデータベース（[パスワード](https://ja.wikipedia.org/wiki/%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89)ファイルなど）、アーカイブフォーマットなど多岐にわたる。単にPOSIXといった場合は、システムコールと[ライブラリ](https://ja.wikipedia.org/wiki/%E3%83%A9%E3%82%A4%E3%83%96%E3%83%A9%E3%83%AA)[関数](https://ja.wikipedia.org/wiki/%E3%82%B5%E3%83%96%E3%83%AB%E3%83%BC%E3%83%81%E3%83%B3)を規定したPOSIX.1 \(IEEE Std 1003.1\)を指すことがある。
>
> C言語のシステムコールとライブラリ関数を規定した規格としては、他に[ANSI](https://ja.wikipedia.org/wiki/%E7%B1%B3%E5%9B%BD%E5%9B%BD%E5%AE%B6%E8%A6%8F%E6%A0%BC%E5%8D%94%E4%BC%9A)/[ISO](https://ja.wikipedia.org/wiki/%E5%9B%BD%E9%9A%9B%E6%A8%99%E6%BA%96%E5%8C%96%E6%A9%9F%E6%A7%8B) C言語とSUS（[Single UNIX Specification](https://ja.wikipedia.org/wiki/Single_UNIX_Specification)、XPG4の後継）がある。各規格の立場の違いにより、これらが含む関数の種類には差がある。数学の記号で表すと、ANSI/ISO C ⊂ POSIX.1 ⊂ SUSとなる。

### 利用

> ### [Unix系](https://ja.wikipedia.org/wiki/Unix%E7%B3%BB)OS以外でも、[Windows NT系](https://ja.wikipedia.org/wiki/Windows_NT%E7%B3%BB)はPOSIX 1.0に準拠しているPOSIX[サブシステム](https://ja.wikipedia.org/wiki/%E3%82%B5%E3%83%96%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0)を搭載しており、POSIXアプリケーションをそのサブシステム上で実行できる[\[2\]](https://ja.wikipedia.org/wiki/POSIX#cite_note-windows-2)。[WTO/TBT協定](https://ja.wikipedia.org/wiki/%E8%B2%BF%E6%98%93%E3%81%AE%E6%8A%80%E8%A1%93%E7%9A%84%E9%9A%9C%E5%AE%B3%E3%81%AB%E9%96%A2%E3%81%99%E3%82%8B%E5%8D%94%E5%AE%9A)では、非関税障壁として工業製品は国際規格を尊重して仕様を規定することを提唱しているため、[米国](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%83%A1%E3%83%AA%E3%82%AB%E5%90%88%E8%A1%86%E5%9B%BD)政府機関のコンピュータシステム導入要件 \([FIPS](https://ja.wikipedia.org/wiki/%E9%80%A3%E9%82%A6%E6%83%85%E5%A0%B1%E5%87%A6%E7%90%86%E6%A8%99%E6%BA%96)\) としてPOSIX準拠であることが規定されていたためである。[\[3\]](https://ja.wikipedia.org/wiki/POSIX#cite_note-fips-3)[Windows 2000](https://ja.wikipedia.org/wiki/Microsoft_Windows_2000)までPOSIXサブシステムを搭載していたが、[Windows XP](https://ja.wikipedia.org/wiki/Microsoft_Windows_XP)からは[Services for UNIX](https://ja.wikipedia.org/wiki/Services_for_UNIX)に同梱の[Interix](https://ja.wikipedia.org/wiki/Interix)サブシステムに役割を譲り、Windows Server 2003 R2や[Windows Vista](https://ja.wikipedia.org/wiki/Windows_Vista)からはSubsystem for UNIX-based Applications \(SUA\)となった[\[2\]](https://ja.wikipedia.org/wiki/POSIX#cite_note-windows-2)。

### 規格

> | ![Question book-4.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/6/64/Question_book-4.svg/50px-Question_book-4.svg.png) | この節の文章は[**不自然な表現、または文意がつかみづらい状態**](https://ja.wikipedia.org/wiki/Template:%E6%97%A5%E6%9C%AC%E8%AA%9E%E8%A1%A8%E7%8F%BE/doc)になっており、修正が必要とされています。（2018年8月） |
> | :--- | :--- |
>
>
> [Linux](https://ja.wikipedia.org/wiki/Linux)の国際標準を制定するにあたり、LinuxとPOSIXの差に関するTRを作成している。
>
> 最初の規格の[テスト](https://ja.wikipedia.org/wiki/%E3%82%BD%E3%83%95%E3%83%88%E3%82%A6%E3%82%A7%E3%82%A2%E3%83%86%E3%82%B9%E3%83%88)スイートは[アメリカ国立標準技術研究所](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%83%A1%E3%83%AA%E3%82%AB%E5%9B%BD%E7%AB%8B%E6%A8%99%E6%BA%96%E6%8A%80%E8%A1%93%E7%A0%94%E7%A9%B6%E6%89%80)がPOSIX Test Suite \(POSIX 1990 version\)としてオープンソースで提供している。

### 注釈

> 1. [**^**](https://ja.wikipedia.org/wiki/POSIX#cite_ref-faq_1-0) “[POSIX 1003.1 FAQ Version 1.12](http://www.opengroup.org/austin/papers/posix_faq.html)” \(2006年2月2日\). 2010年12月29日閲覧。
> 2. ^ [**a**](https://ja.wikipedia.org/wiki/POSIX#cite_ref-windows_2-0) [**b**](https://ja.wikipedia.org/wiki/POSIX#cite_ref-windows_2-1) “[POSIX and UNIX Support in Windows](https://social.technet.microsoft.com/wiki/contents/articles/10224.posix-and-unix-support-in-windows.aspx)”. 2018年8月10日閲覧。
> 3. [**^**](https://ja.wikipedia.org/wiki/POSIX#cite_ref-fips_3-0) [Federal Information Processing Standard \(FIPS\) 151-2](https://web.archive.org/web/20140220130516/http://www.itl.nist.gov/fipspubs/fip151-2.htm) - [ウェイバックマシン](https://ja.wikipedia.org/wiki/%E3%82%A6%E3%82%A7%E3%82%A4%E3%83%90%E3%83%83%E3%82%AF%E3%83%9E%E3%82%B7%E3%83%B3)（2014年2月20日アーカイブ分）





