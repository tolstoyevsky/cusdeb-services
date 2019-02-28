# MediaWiki

<p align="center">
    <img src="logo.svg" width="400">
</p>

MediaWiki is one of the most famous wiki engines. It's best known for being used as a base for [Wikipedia](http://wikipedia.org).

<table>
  <tr>
    <td align="center" colspan="2"><b>MediaWiki</b></td>
  </tr>
  <tr>
    <td>Version</td>
    <td><a href="https://mediawiki.org/wiki/MediaWiki_1.31">1.31</a></td>
  </tr>
  <tr>
    <td>Release date</td>
    <td>13 Jun 2018</td>
  </tr>
  <tr>
    <td>Port</td>
    <td>8004</td>
  </tr>
  <tr>
    <td>Data volume</td>
    <td>
        <code>/srv/mediawiki/deleted:/var/www/w/deleted</code><br>
        <code>/srv/mediawiki/images:/var/www/w/images</code>
    </td>
  </tr>
  <tr>
    <td valign="top">Base images</td>
    <td>
        <code>cusdeb/alpine3.9:armhf</code> (for <code>armhf</code> port)<br>
        <code>cusdeb/alpine3.9:amd64</code> (for <code>amd64</code> port)
    </td>
  </tr>
</table>

## Features

* Nginx [1.14.2](http://nginx.org/en/CHANGES-1.14) and PHP [7.2.14](http://php.net/ChangeLog-7.php#7.2.14).
* [VisualEditor](https://mediawiki.org/wiki/Extension:VisualEditor) extension which allows editing pages as rich content.

## Configuration

`docker-compose.yml` supports the following parameters.

| Parameter | Description | Default |
| --- | --- | --- |
| PORT                    | Port wiki is available on | 8004 |
| WG_SITENAME             | Wiki name | My KB |
| WG_META_NAMESPACE       | [Name](https://mediawiki.org/wiki/Manual:$wgMetaNamespace) used for the project namespace | My_KB |
| WG_PROTOCOL             | Protocol which is used for accessing wiki (`http` and `https`) | `http` |
| WG_SERVER               | [Domain or IP](https://mediawiki.org/wiki/Manual:$wgServer) of the wiki host | 127.0.0.1:8004 |
| WG_EMERGENCY_CONTACT    | Wiki [admin email address](https://mediawiki.org/wiki/Manual:$wgEmergencyContact) | username@domain.com |
| WG_PASSWORD_SENDER      | [Password reminder email address](https://mediawiki.org/wiki/Manual:$wgPasswordSender) | username@domain.com |
| WG_DB_SERVER            | [Database server host](https://mediawiki.org/wiki/Manual:$wgDBserver) | 127.0.0.1:33061 |
| WG_DB_NAME              | [Database name](https://mediawiki.org/wiki/Manual:$wgDBname) | knowledge_base |
| WG_DB_USER              | [Database user](https://mediawiki.org/wiki/Manual:$wgDBuser) | root |
| WG_DB_PASSWORD          | [Database password](https://mediawiki.org/wiki/Manual:$wgDBpassword) | cusdeb |
| ALLOW_ACCOUNT_CREATION  | Allows users to create accounts (`true` and `false`) | `true` |
| ALLOW_ACCOUNT_EDITING   | Allows users to edit their accounts (`true` and `false`) | `true` |
| ALLOW_ANONYMOUS_READING | Allows users to read wiki anonymously (`true` and `false`). If the parameter is `false`, wiki is **private** | `true` |
| ALLOW_ANONYMOUS_EDITING | Allows users to edit wiki anonymously (`true` and `false`) | `true` |
| PARSOID_DOMAIN          | Domain of the Parsoid host (the value must be equal to the `PARSOID_DOMAIN` parameter from the [Parsoid](https://github.com/tolstoyevsky/mmb/tree/master/parsoid) Docker image) | parsoid |
| PARSOID_HOST            | Domain or IP of the Parsoid host | http://127.0.0.1:8005 |

Note, that commenting the `PARSOID_HOST`, `PARSOID_PORT` and `PARSOID_PROTOCOL` parameters deactivates the [VisualEditor](https://mediawiki.org/wiki/Extension:VisualEditor) extension. By default, the parameters are uncommented.

## How to change logo

Provide a square logo named `kblogo.png` which is 135x135px or 150x150px. Note that running the container without providing any logo causes creating the `kblogo.png` directory. Don't be confused. Simply remove the directory before copying a real logo to `mediawiki`.
