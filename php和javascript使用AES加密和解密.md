## php和javascript使用AES加密和解密.md  

在前端和后端的数据交互中，很多情况会使用到AES加密和解密。  
下面就来讲解一下经典的场景：  
&emsp;&emsp;1、前端使用javascript进行AES加密，后端使用php进行AES解密；   
&emsp;&emsp;2、 后端使用php进行AES加密，前端使用javascript进行AES解密。    
    

### javascript的AES加解密函数
```
/**
 * 需引入 CryptoJS
 * 加密
 * @param word 需加密信息
 * @param key 秘钥
 * @returns {*}
 */
function encrypt(word, _key) {
	var key = CryptoJS.enc.Utf8.parse(_key);
	var srcs = CryptoJS.enc.Utf8.parse(word);
	var encrypted = CryptoJS.AES.encrypt(srcs, key, {
		mode: CryptoJS.mode.ECB,
		padding: CryptoJS.pad.Pkcs7
	});
	return encrypted.toString();
}

/**
 * 需引入 CryptoJS
 * 解密
 * @param word 需解密信息
 * @param key 秘钥
 * @returns {*}
 */
function decrypt(word, _key) {
	var key = CryptoJS.enc.Utf8.parse(_key);
	var decrypt = CryptoJS.AES.decrypt(word, key, {
		mode: CryptoJS.mode.ECB,
		padding: CryptoJS.pad.Pkcs7
	});
	return CryptoJS.enc.Utf8.stringify(decrypt).toString();
}
```

### php的AES加解密函数
```
class AES
{
  /**
   * @param string $string 需要加密的字符串
   * @param string $key 密钥
   * @return string
   */
  public static function encrypt($string, $key)
  {
    $data = openssl_encrypt($string, 'AES-128-ECB', $key, OPENSSL_RAW_DATA);
    return base64_encode($data);
  }

  /**
   * @param string $string 需要解密的字符串
   * @param string $key 密钥
   * @return string
   */
  public static function decrypt($string, $key)
  {
    return openssl_decrypt(base64_decode($string), 'AES-128-ECB', $key, OPENSSL_RAW_DATA);
  }
}
```
