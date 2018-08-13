# Rocket.Chat Hubot adapter

Rocket.Chat Hubot adapter is the way to integrate [Hubot](https://hubot.github.com) with [Rocket.Chat](https://rocket.chat). This is one of the third-party [adapters](https://hubot.github.com/docs/adapters/).

<table>
  <tr>
    <td align="center" colspan="2"><b>Rocket.Chat Hubot adapter</b></td>
  </tr>
  <tr>
    <td>Version</td>
    <td><a href="https://github.com/RocketChat/hubot-rocketchat/releases/tag/v1.0.11">1.0.11</a></td>
  </tr>
  <tr>
    <td>Release date</td>
    <td>07 Aug 2017</td>
  </tr>
  <tr>
    <td valign="top">Base images</td>
    <td>
        <code>cusdeb/alpine3.7:armhf</code> (for <code>armhf</code> port)<br>
        <code>cusdeb/alpine3.7:amd64</code> (for <code>amd64</code> port)
    </td>
  </tr>
</table>

## Table of Contents

* [Features](#features)
* [Installation](#installation)
* [Configuration](#configuration)
* [Installing external scripts](#installing-external-scripts)

## Features

The following set of scripts makes the bot capable of doing all sort of things:

* [hubot-auth](https://github.com/hubot-scripts/hubot-auth) – allows assigning roles to users and restricting command access in other scripts.
* [hubot-happy-birthder](https://github.com/tolstoyevsky/hubot-happy-birthder) – writes birthday messages to users.
* [hubot-help](https://github.com/hubotio/hubot-help) – shows available commands.
* [hubot-pugme](https://github.com/hubot-scripts/hubot-pugme) – shows random pictures with pugs.
* [hubot-reaction](https://github.com/hubot-scripts/hubot-reaction) – interacts with [replygif.net](http://replygif.net).
* [hubot-redis-brain](https://github.com/hubotio/hubot-redis-brain) – allows using Redis as an alternative storage backend for the Hubot in-memory key-value storage exposed as `robot.brain`.
* [hubot-thecat](https://github.com/tenten0213/hubot-thecat) – interacts with [The Cat API](http://thecatapi.com).
* [hubot-thesimpsons](https://github.com/hubot-scripts/hubot-thesimpsons) – generates the quotes and images related to The Simpsons.
* [hubot-vote-or-die](https://github.com/tolstoyevsky/hubot-vote-or-die) – allows building polls.

## Installation

Read the [Getting Started](https://github.com/tolstoyevsky/mmb#getting-started) section to learn how to install this or other services.

## Configuration

`docker-compose.yml` supports the following parameters.

<table>
  <tr>
    <td align="center"><b>Parameter</b></td>
    <td align="center"><b>Description</b></td>
    <td align="center"><b>Default</b></td>
  </tr>
  <tr>
    <td align="center" colspan="3"><b>Rocket.Chat Hubot adapter</b></td>
  </tr>
  <tr>
    <td>ROCKETCHAT_URL</td>
    <td>Domain or IP of the Rocket.Chat host.</td>
    <td>http://127.0.0.1:8006</td>
  </tr>
  <tr>
    <td>ROCKETCHAT_ROOM</td>
    <td>Comma-separated list containing the channels the bot must listen in.</td>
    <td></td>
  </tr>
  <tr>
    <td>ROCKETCHAT_USER</td>
    <td>Name of the user on whose behalf the bot works. Note, that the user <b>must</b> exist before running the adapter.</td>
    <td>meeseeks</td>
  </tr>
  <tr>
    <td>ROCKETCHAT_PASSWORD</td>
    <td>Password of the user on whose behalf the bot works.</td>
    <td>pass</td>
  </tr>
  <tr>
    <td>EXTERNAL_SCRIPTS</td>
    <td colspan="2">Comma-separated list of the scripts which must be installed. Using the parameter it's possible to install scripts either from the NPM registry or from the specified Git repository (<a href="#installing-external-scripts">read more</a>).<br>
By default, only <code>hubot-help</code> is installed via the parameter. However, if the container runs through <code>docker-compse</code> using <code>docker-compose.yml</code> (or its variations), the scripts from the list <a href="#features">above</a> will be installed.</td>
  </tr>
  <tr>
    <td>HUBOT_NAME</td>
    <td>Programmatic name for listeners.</td>
    <td>bot</td>
  </tr>
  <tr>
    <td>LISTEN_ON_ALL_PUBLIC</td>
    <td>Respond listens in all public channels (<code>true</code> or <code>false</code>)</td>
    <td><code>true</code></td>
  </tr>
  <tr>
    <td>TZ</td>
    <td>Time zone. See all the possible values for the parameter <a href="https://en.wikipedia.org/wiki/List_of_tz_database_time_zones">here</a>.</td>
    <td>Europe/Moscow</td>
  </tr>
  <tr>
    <td align="center" colspan="3"><b>hubot-auth</b></td>
  </tr>
  <tr>
    <td>HUBOT_AUTH_ADMIN</td>
    <td>Comma-separated list containing the ids of the users who must have the admin rore. To get to know your user id, use the bot command <code>what is my id</code>.</td>
    <td></td>
  </tr>
  <tr>
    <td align="center" colspan="3"><b>hubot-happy-birthder</b></td>
  </tr>
  <tr>
    <td colspan="3"><code>TENOR_API_KEY</code> is the only <b>mandatory</b> parameter both in this script and in the Docker image. The script will fail if the parameter is equal to an empty string (which it is by default).<br>See the description for all the parameters related to the script in its original <a href="https://github.com/tolstoyevsky/hubot-happy-birthder">README</a>.</td>
  </tr>
  <tr>
    <td align="center" colspan="3"><b>hubot-redis-brain</b></td>
  </tr>
  <tr>
    <td>REDIS_URL</td>
    <td>Domain or IP of the Redis host.</td>
    <td>redis://127.0.0.1:16379</td>
  </tr>
</table>

## Installing external scripts

`EXTERNAL_SCRIPTS` is a comma-separated list of the scripts which must be installed. To install a script from the official NPM registry, simply specify its name in the list. To install a script from its GitHub repository, use the following format: `git:github-username/repo-name`. In this case the script will be installed from the `master` branch. To specify a different branch follow the format: `git:github-username/repo-name@target-branch`.
