## Semcms Shop V4.2 后台文件上传getshell

On **SEMCMS_Upfile.php**

![Cow1](https://github.com/xlccccc/vuln/blob/master/Semcms/Semcms%20V4.2.assets/image-20230321203051424.png "Cow1")
Regular matching for white lists can be passed as long as the **file suffix has the white list**



It is possible to **control the file name**, and the suffix is spliced from the previously obtained file suffix

**第一次上传**

`wname=shell.jpg.php: filename=test.jpg` 

At this point, after splicing, `$newname=shell.jpg.php:.jpg` is displayed. On Windows platforms, the following `:` file name will change to `shell.jpg.php` due to non-compliance with the rules, but the php point to `shell.jpg.php:.jpg`, so the file content cannot be transferred in. At this point, an empty php file has been constructed

![Cow1](https://github.com/xlccccc/vuln/blob/master/Semcms/Semcms%20V4.2.assets/image-20230321204300443.png "Cow1")
![Cow1](https://github.com/xlccccc/vuln/blob/master/Semcms/Semcms%20V4.2.assets/image-20230321204245267.png "Cow1")
**第二次上传**

`wname=shell filename=test.jpg<<<`

After splicing, `$newname=shell.jpg<<<`, while `<` in Windows is equivalent to a wildcard character, which will match `shell.jpg.php`

To transfer the file content to `shell.jpg.php`

![Cow1](https://github.com/xlccccc/vuln/blob/master/Semcms/Semcms%20V4.2.assets/image-20230321204400480.png "Cow1")
![Cow1](https://github.com/xlccccc/vuln/blob/master/Semcms/Semcms%20V4.2.assets/image-20230321204349453.png "Cow1")
After uploading any php file, you can try getshell