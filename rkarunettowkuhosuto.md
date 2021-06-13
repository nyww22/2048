# ローカルネットワーク内ホスト名解決

{% embed url="http://independence-sys.net/main/?p=2116" %}

{% embed url="https://www.openaudiolab.com/2019-05-18-hostnames-vs-static-ip-adresses-jp/" %}

{% embed url="https://www.it-swarm-ja.tech/ja/networking/%E3%83%9B%E3%82%B9%E3%83%88%E5%90%8D%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%97%E3%81%A6lan%E3%81%8B%E3%82%89%E3%83%9E%E3%82%B7%E3%83%B3%E3%81%AB%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B9%E3%81%A7%E3%81%8D%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95/957202450/" %}

{% embed url="https://qiita.com/maccadoo/items/48ace84f8aca030a12f1" %}

> ## Windows, Mac OS X, Linux間でDNSを使わずにホスト名を解決する方法：mDNS編
>
>  [Nakano Kieta](https://typex2.wordpress.com/author/typex20/)  [Apple](https://typex2.wordpress.com/category/apple/)・[Linux](https://typex2.wordpress.com/category/linux/)・[Mac OS X](https://typex2.wordpress.com/category/apple/mac-os-x/)・[Microsoft](https://typex2.wordpress.com/category/microsoft/)・[Windows](https://typex2.wordpress.com/category/microsoft/windows/)  2009-09-27
>
> NetBIOS over TCP/IP編に引き続き、mDNSを使用してWindows, Mac OS X, Linux間でホスト名を解決する方法についてです。
>
> 以下、長文となります。
>
> まずはmDNS関連のサーベイから。
>
> <table>
>   <thead>
>     <tr>
>       <th style="text-align:left"></th>
>       <th style="text-align:left">mDNS</th>
>       <th style="text-align:left">LLMNR</th>
>     </tr>
>   </thead>
>   <tbody>
>     <tr>
>       <td style="text-align:left">&#x6982;&#x8981;</td>
>       <td style="text-align:left">
>         <p><a href="http://wiki.osdev.info/?mDNS">mDNS &#x2013; osdev-j (MMA)</a>
>         </p>
>         <p><a href="http://wiki.osdev.info/?%A5%CD%A5%C3%A5%C8%A5%EF%A1%BC%A5%AF%A5%D7%A5%ED%A5%C8%A5%B3%A5%EB">&#x30CD;&#x30C3;&#x30C8;&#x30EF;&#x30FC;&#x30AF;&#x30D7;&#x30ED;&#x30C8;&#x30B3;&#x30EB;</a> 
>           <a
>           href="http://wiki.osdev.info/?Rendezvous">Rendezvous</a> <a href="http://wiki.osdev.info/?DNS">DNS</a>  <a href="http://wiki.osdev.info/?DNS-SD">DNS-SD</a>
>         </p>
>         <p><a href="http://www.multicastdns.org/">http://www.multicastdns.org/</a> &#x2013;
>           &#x672C;&#x5BB6;</p>
>         <p>Multicast DNS&#x3002;DNS&#x30D1;&#x30B1;&#x30C3;&#x30C8;&#x3092;<a href="http://wiki.osdev.info/?IP%A5%DE%A5%EB%A5%C1%A5%AD%A5%E3%A5%B9%A5%C8">IP&#x30DE;&#x30EB;&#x30C1;&#x30AD;&#x30E3;&#x30B9;&#x30C8;</a>&#x3067;&#x6D41;&#x3059;&#x3002;&#x6A19;&#x6E96;&#x30DD;&#x30FC;&#x30C8;&#x306F;5353&#x3002;</p>
>         <p><a href="http://wiki.osdev.info/?DNS-SD">DNS-SD</a>&#x306B;&#x3088;&#x308B;
>           <a
>           href="http://wiki.osdev.info/?%A5%B5%A1%BC%A5%D3%A5%B9%A5%EB%A5%C3%A5%AF%A5%A2%A5%C3%A5%D7">&#x30B5;&#x30FC;&#x30D3;&#x30B9;&#x30EB;&#x30C3;&#x30AF;&#x30A2;&#x30C3;&#x30D7;</a>&#x306B;&#x7528;&#x3044;&#x3089;&#x308C;&#x308B;&#x3002;</p>
>         <p>&#x2192;<a href="http://wiki.osdev.info/?DNS-SD">DNS-SD</a>
>         </p>
>       </td>
>       <td style="text-align:left">
>         <p><a href="http://wiki.osdev.info/?LLMNR">LLMNR &#x2013; osdev-j (MMA)</a>
>         </p>
>         <p><a href="http://tools.ietf.org/html/rfc4795">RFC:4795</a>&#x3002;<a href="http://wiki.osdev.info/?mDNS">mDNS</a>&#x306B;&#x76F8;&#x5F53;&#x3059;&#x308B;&#x4F4D;&#x7F6E;&#x4ED8;&#x3002;</p>
>         <p><a href="http://wiki.osdev.info/?UDP">UDP</a>&#x30DD;&#x30FC;&#x30C8;5355&#x3001;IPv4&#x30DE;&#x30EB;&#x30C1;&#x30AD;&#x30E3;&#x30B9;&#x30C8;224.0.0.252&#x3001;IPv6&#x30DE;&#x30EB;&#x30C1;&#x30AD;&#x30E3;&#x30B9;&#x30C8;FF02:0:0:0:0:0:1:3&#x3002;&#x30D1;&#x30B1;&#x30C3;&#x30C8;&#x30D5;&#x30A9;&#x30FC;&#x30DE;&#x30C3;&#x30C8;&#x306F;
>           <a
>           href="http://wiki.osdev.info/?DNS">DNS</a>&#x3068;&#x540C;&#x69D8;&#x3002;</p>
>       </td>
>     </tr>
>     <tr>
>       <td style="text-align:left">&#x5BFE;&#x5FDC;&#x88FD;&#x54C1;</td>
>       <td style="text-align:left">
>         <p>&#x30FB;Apple&#x306E;Bonjour&#x306F;mDNS&#x3092;&#x4F7F;&#x7528;&#x3057;&#x3066;&#x3044;&#x308B;&#x3002;&#xFF08;Mac
>           OS X, iTunes, iPhone/iPod touch&#x306A;&#x3069;&#xFF09;
>           <br /><a href="http://ja.wikipedia.org/wiki/Bonjour">Bonjour &#x2013; Wikipedia</a>
>         </p>
>         <p>&#x30FB;Linux&#x306E;avahi&#x304C;&#x5BFE;&#x5FDC;&#x3057;&#x3066;&#x3044;&#x308B;&#x306E;&#x306F;mDNS&#x3002;</p>
>       </td>
>       <td style="text-align:left">&#x30FB;Windows Vista&#x4EE5;&#x964D;&#x3067;&#x3001;LLMNR&#x306B;&#x5BFE;&#x5FDC;&#x3057;&#x3066;&#x3044;&#x308B;&#x3002;</td>
>     </tr>
>   </tbody>
> </table>
>
> ・Apple製品で対応しているのはmDNSで、Microsoft製品で対応しているのはLLMNR。
>
> ・AppleとMicrosoftが解決しようとしている問題は同じですが、mDNSとLLMNRは上記を見てもわかるとおり、使用するポート番号が異なるし、互換性がありません。大人の事情ってやつでしょうか。
>
> **○mDNSを使用できるようにする。**
>
> ということで、以下の設定を行えば、Windows, Mac OS X, Linuxから、「ホスト名.local」でホスト名の解決が出来るようになります。
>
> ■Windows
>
> 最新のiTunesをインストールするか、[Bonjour for Windows](http://support.apple.com/downloads/Bonjour_for_Windows?viewlocale=ja_JP)をインストールします。
>
> Bonjourがインストールされていれば特に何もしなくてもmDNSで「ホスト名.local」でホスト名の解決ができるようになります。
>
> さて、ここで気になるmDNSとLLMNRの競合の問題です。
>
> 以下によると、
>
> [Catra’s Diary \[2009-07\]](http://homepage2.nifty.com/Catra/diary/200907.html#071200)
>
> > ここで Vista になって IPv6 対応が進んだことにより、 Vista 単体でも Link-Local Multicast Name Resolution \(LLMNR\) を搭載。 しかし、実装している範囲が Bonjour とは異なっており、
> >
> > １．「ホスト名.local」についての問い合わせに応答しない  
> > ２．他のホストに対する「ホスト名.local」名前問い合わせは内部で「ホスト名」の問い合わせに変換して LLMNR で問い合わせる
> >
> > という謎な仕様になっている。このため、
> >
> > １．他からの「ホスト名.local」問い合わせに応答しない  
> > ２．他ホストが応答するはずの「ホスト名.local」問い合わせが変換され「ホスト名」になるため、他ホストの名前問い合わせもできない \(「ホスト名」を名前解決するのは NetBIOS over TCP/IP の仕事で、LLMNR \(avahi\)で対応できない\)
>
> ・まず、avahiはLLMNRは対応していないはず？
>
> ・次に、Windows Vista, Windows 7は、標準ではmDNSに対応していないので、mDNSによる名前問い合わせ、応答が出来ません。
>
> －mDNSによる他ホストに対する「ホスト名.local」の名前問い合わせができない。  
> －mDNSによる他ホストからの「ホスト名.local」問い合わせに応答しない。  
> （他ホストではmDNSによる「ホスト名.local」の名前問い合わせできない）
>
> また、以下によると、  
> [Link-Local Multicast Name Resolution- The Cable Guy, November 2006](http://technet.microsoft.com/ja-jp/library/bb878128.aspx)  
> （[英語版](http://technet.microsoft.com/en-us/library/bb878128.aspx)）
>
> Windows Vista, Windows 7は、
>
> ・正式なホスト名として「ホスト名.local」をサポートしていない。
>
> ・「ホスト名.local」に慣れているユーザの利便性のために、他ホストに対する単一の「ホスト名.local」の名前問い合わせを受け付けると、
>
> LLMNRにより単一の「ホスト名」で名前問い合わせしようとするので、LLMNRに対応していない機器では名前解決ができません。
>
> Windows 7 RCの挙動を見ている感じでは、「ホスト名.local」の名前問い合わせをすると、LLMNRで名前解決が出来なければ中断してしまい、NetBIOS over TCP/IPで名前問い合わせをしていないようです。
>
> ただし、最初から単一の「ホスト名」で名前問い合わせをすれば、
>
> 「LLMNR」→「NetBIOS over TCP/IP」
>
> の順番で名前問い合わせを行おうとするので、NetBIOS over TCP/IPに対応している機器であればホスト名を解決できます。
>
> ・LLMNRにより他ホストから「ホスト名.local」という名前問い合わせがきても応答しないので、他ホストではLLMNRによる「ホスト名.local」の名前解決はできません。
>
> Windows 7 RCでの詳しい動作を見てみます。
>
> | Windows7 RC標準のName Space Provider \(mswsock.dll\) | BonjourのName Space Provider \(mdnsNSP.dll\) |
> | :--- | :--- |
> | \HKEY\_LOCAL\_MACHINE\SYSTEM \CurrentControlSet\service \WinSock2\Parameters \NameSpace\_Catalog5\Catalog\_Entries6400000000007 | \HKEY\_LOCAL\_MACHINE\SYSTEM \CurrentControlSet\service \WinSock2\Parameters \NameSpace\_Catalog5\Catalog\_Entries6400000000007 |
> | SupportedNameSpace=12（DNS） | SupportedNameSpace=12（DNS） |
> | [![WS000022](https://typex2.files.wordpress.com/2009/09/ws000022_thumb.jpg?w=244&h=149)](https://typex2.files.wordpress.com/2009/09/ws000022.jpg) | [![WS000021](https://typex2.files.wordpress.com/2009/09/ws000021_thumb.jpg?w=244&h=149)](https://typex2.files.wordpress.com/2009/09/ws000021.jpg) |
>
> Windows 7 RCでは、DNSのWinsock2のName Space Providerであるmswsock.dllが１つあります。
>
> Bonjourをインストールすると、DNSのWinsock2のName Space Providerとして、mdnsNSP.dllが追加されます。
>
> ・mswsock.dllとmdnsNSP.dllを有効にして「ping ホスト名.local」を実行すると、レスポンスが返ってくるのにしばらく時間がかかります。
>
> ・mswsock.dllを無効、mdnsNSP.dllが有効にして「ping ホスト名.local」を実行すると、すぐにレスポンスが返ってきます。
>
> このことから、mswsock.dll（LLMNR） → mdnsNSP.dll（mDNS）の順番で名前問い合わせを行っているのではないかと推測できます。
>
> 実装としては、こんな感じになっているのではないかと思われます。
>
> ・「ホスト名.local」の名前問い合わせがあると、WinSock2のDNSのName Space Providerのみが呼び出される。
>
> ・WinSock2のDNSのName Space Providerの  
> mswsock.dll（LLMNR） → mdnsNSP.dll（mDNS）の順番で呼び出される。
>
> （ただし、LLMNRで名前解決が出来なかったらNetBIOS over TCP/IPでは名前問い合わせを行わない）
>
> **まとめると、Windows Vista, Windows 7では、**
>
> **・単一の「ホスト名」あるいは「ホスト名.local」の名前問い合わせは、LLMNRを使用する。**
>
> **・「ホスト名.local」の名前問い合わせは、LLMNRのみで名前問い合わせを行い、NetBIOS over TCP/IPでは名前問い合わせを行わない。**
>
> **・単一の「ホスト名」の名前問い合わせは、「LLMNR」→「NetBIOS over TCP/IP」で名前問い合わせを行う。**
>
> **・上記以外の名前問い合わせ（単一の「ホスト名」と「ホスト名.local」を除く）はDNSを使用する。**
>
> **・他ホストからのLLMNRによる名前問い合わせでは「ホスト名.local」は応答しない。  
> （Windows Vista, Windows 7では正式なホスト名としてサポートしてないため）**
>
> ちなみに、Windows Vista以降でLLMNRを無効にする方法は、以下のレジストリを0x0にするとあります。（本当に有効なのかどうか真偽は不明です）
>
> [EnableMulticast – Microsoft TechNet Search](http://social.technet.microsoft.com/Search/en-US?query=EnableMulticast&ac=3)  
> [Ability to disable LLMNR- – Vista Forums](http://www.vistax64.com/vista-networking-sharing/95027-ability-disable-llmnr.html)
>
> > HKLM\Software\Policies\Microsoft\Windows NT\DNSClient!EnableMulticast（DWORD値です）
>
> ■Mac OS X
>
> 特に設定する必要はありません。標準で使用できます。
>
> ■Linux
>
> apt-get install avahiを実行してavahiをインストールします。
>
> 単にmDNSでホスト名を解決したいだけなら特に設定は必要ありません。
>
> あとは、/etc/nsswitch.confのホスト行にmDNSを使用するための設定を追加するだけです。
>
> > hosts:          files wins mdns4\_minimal \[NOTFOUND=return\] dns mdns4

