# Install Sublime Text3

### Summary

{% embed url="https://qiita.com/riv/items/e8de0aa218d12429206a" %}



### install Package Control

```text
import urllib.request,os,hashlib; h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

```



#### （Qitta記載箇所の誤り訂正）

> **１．指定箇所にDefaultディレクトリを作成**
>
> 下記の場所に移動します。（今回はUbuntu環境です。）
>
> ```text
> cd ./.config/sublime-text-3/Packages/
> ```
>
> すると、「Japanize」のディレクトリがあり、「Default」ディレクトリは存在しないはずです。  
> そこでまずは、この場所にDefaultディレクトリを作成します。
>
> ```text
> mkdir Default
> ```



