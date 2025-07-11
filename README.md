# Stagesoft project FormitGo

<img src="https://stagesoft.github.io/img/formitgo.jpg" height="200">


## About

**FormitGo** and the **cuems** suite is a new open source software project from [Stagelab](https://www.stagelab.coop).

<img src="https://stagesoft.github.io/img/original_fons_transparent.png" height=100>

**cuems** suite will not only manage cues but also network connected external devices.

Its main audience is theatre and live entertainment technicians.

cuems will try to reuse and improve other open source projects such as:

* [xjadeo](https://github.com/stagesoft/xjadeo)

cuems will generate new projects from scratch like:

* [cuems-engine](https://github.com/stagesoft/cuems-engine)
* [cuems-editor](https://github.com/stagesoft/cuems-editor)
* [cuems-utils](https://github.com/stagesoft/cuems-utils)
* [libmtcmaster](https://github.com/stagesoft/libmtcmaster)
* [cuems-audioplayer](https://github.com/stagesoft/cuems-audioplayer)


## Documentation API

All technical documentation is available at it's corresponding GitHub Pages site as `https://stagesoft.github.io/<REPOSITORY_NAME>/`


## Stagesoft packages

You can find our repositories at [Stagesoft Github page](https://github.com/stagesoft).

And our packages repository at [Stagesoft package repository](https://repo.stagelab.coop)

(debian 10 packages, amd64, dbgsym and source)

______

**Instructions to add the repo to debian 10 buster:**

### via keyring directory (recommended)

Add the signing key to your keyring:
```bash
> wget -O- https://repo.stagelab.coop/repo.stagelab.key | \
    gpg --dearmor --yes \
    --output /usr/share/keyrings/stagelab.gpg

> echo "deb [arch=amd64 signed-by=/usr/share/keyrings/stagelab.gpg] https://repo.stagelab.coop/debian buster main" | \
    tee -a /etc/apt/sources.list.d/stagelab.list
```

For non-root users, use `sudo` before the `gpg` and `tee` commands above.

For more information on signing packages, see the [Debian wiki](https://wiki.debian.org/SecureApt#Settingupasecureaptrepository)


### via apt-key (old way)
First add the key used to sing the packages & repo:

`wget -q -O - https://repo.stagelab.coop/repo.stagelab.key |sudo apt-key add -`

Then add the repo to a new sources.list.d/ file:

`sudo wget -O /etc/apt/sources.list.d/stagelab.list https://repo.stagelab.coop/stagelab.list`

Or manually:

`deb https://repo.stagelab.coop/debian buster main`

`deb-src https://repo.stagelab.coop/debian buster main`
____


## Packages

For a complete list of software under development by Stagelab, see [Stagesoft GitHub page](https://github.com/stagesoft).

list of packages currently on the repository:

(work in progress, unstable packages at the moment for testing purpouses)
* cuems-audioplayer
* libmtcmaster
* xjadeo
* jackd2
* libossia
* cmake
 
## Funding

This project is promoted by:

![promoted_by_gencat](https://stagesoft.github.io/img/generalitat.svg)

![promoted_by_ess](https://stagesoft.github.io/img/economiasocial.svg)

This project is funded by:

![funded_by_ministerio](https://stagesoft.github.io/img/ministerio.svg)

This project had the initial collaboration of [bTactic](https://www.btactic.com):

![bTactic logo](https://www.btactic.com/wp-content/uploads/2018/10/logo-btactic.png)
