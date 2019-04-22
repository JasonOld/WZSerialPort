# WzSerialPort

*源码为UTF-8带BOM格式，建议用该编码格式打开*



**Windows、Linux上的C++串口库，封装系统的原生API**

**参考本项目使用**

---

## Windows上常见问题：
* 在Windows上，要打开COM10以后的串口（包括COM10），串口名称不再是“COM10”，而是“\\\\.\\COM10”，因此在open函数中，如果是COM10及以后的串口，串口名（假设当前要打开COM10）应该写“\\\\\\\\.\\\\COM10”，其中“\\\\\\\\.\\\\”为“\\\\.\\”的转义。
* 在visual studio的项目中，编译报错，错误指向WzSerialPort.cpp的157行、211行的问题：
``` cpp
157|    m_osWrite.hEvent = CreateEvent(NULL, TRUE, FALSE, L"WriteEvent");
```
``` cpp
211|    m_osRead.hEvent = CreateEvent(NULL, TRUE, FALSE, L"ReadEvent");
```
&emsp;&emsp;&emsp;导致这个编译报错的其实是VS的字符集设置所导致的。①将字符集改为“使用Unicode字符集”即可，②或者将 L"WriteEvent" 和 L"ReadEvent" 前面的 L 删除掉也可以。
**总而言之吧，这是微软的要求，字符集设置为 “使用Unicode字符集” 时需要加在字符串前加 L 先将 char\* 转为 wchar_t\* 再转为 LPCWSTR，字符集设置为 “使用多字节字符集” 时，则无需将 char\* 转为 wchar_t\* ，可直接转为LPCWSTR，因此无需加 L**

---

## Linux上的常见问题：
* 串口无法打开，可能是由于权限的问题，sudo一般可解决这个问题。
* 读串口的时候，有阻塞的现象，经测试，仅仅是Ubuntu18.04上出现来该问题，这可能是虚拟串口的原因，后续使用实际串口中如果仍有该问题，后续再更新...s

---

