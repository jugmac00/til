# How can you check the support status for installed packages?

When you install a package from the package repository on Ubuntu LTS,
the package will be maintained for 5 years, right?

**No!**

At least, not necessarily.

Basically, you need to understand that there are different repository types for Ubuntu:

| type       | maintained by canonical | floss | guaranteed support in years|
| -----------|:-----------------------:| ------| ---------------------------| 
| main | yes | yes | 5 |
| restricted | yes | no | ? |
| universe | no | yes | ? |
| multiverse | no | no | ? |

(There are more than those listed (e.g. ppa..., but let's keep it "simple" for now)

As you can see, packages from the `main` repository will be maintained for five years,
but there are many question marks above.

Let's try to bring some light into darkness.

## Ubuntu 18.04 LTS

When you are on Ubuntu 18.04, you can simply enter the following command:

```
$ ubuntu-support-status
Support status summary of 'server':

You have 523 packages (100.0%) supported until April 2023 (Canonical - 5y)

You have 0 packages (0.0%) that can not/no-longer be downloaded
You have 0 packages (0.0%) that are unsupported

Run with --show-unsupported, --show-supported or --show-all to see more details
```

This is the output of virtual machine with only a few services.

Likely, the output of your desktop / laptop will look differently - at least mine does!

```
Support status summary of 'jugmac00-XPS-13-9370':

You have 1928 packages (76.2%) supported until April 2023 (Canonical - 5y)
You have 162 packages (6.4%) supported until April 2021 (Community - 3y)
You have 3 packages (0.1%) supported until April 2021 (Canonical - 3y)

You have 24 packages (0.9%) that can not/no-longer be downloaded
You have 412 packages (16.3%) that are unsupported

Run with --show-unsupported, --show-supported or --show-all to see more details
```
Holy! I know what I will do on the weekend!

You can use the suggested options to show more information, e.g. a detailed list of packages and their support status.

## Ubuntu 20.04 LTS

For reasons the above command was deprecated and removed for Ubuntu 20.04 LTS.

Luckily, there is a replacement command:

```
$ ubuntu-security-status
586 packages installed, of which:
577 receive package updates with LTS until 4/2025
  6 could receive security updates with ESM Apps until 4/2030
  3 packages are from third parties

Packages from third parties are not provided by the official Ubuntu
archive, for example packages from Personal Package Archives in
Launchpad.
For more information on the packages, run 'ubuntu-security-status
--thirdparty'.

Enable Extended Security Maintenance (ESM Apps) to get 0 security
updates (so far) and enable coverage of 6 packages.
```

This is the output of another virtual machine, where I installed Docker,
thus the "3 packages are from third parties".

All installed packages from the official repositories will be supported until 2023 - yeah!

For the third party packages, you have to take care yourself.

## open questions

Ok, but how would I know in advance how long a package will be maintained, given it is not provided by `main`?

e.g. how long would `etherwake` be maintained?

I have not found an answer yet.

Maybe you can help? Drop me a line, hit me on Twitter, or create a pull request.

## conclusion

- do not count on "it is in the repository, so it is maintained"
- try to use packages from `main`
- regularly check your packages with above mentioned commands

## bonus

[Marius](https://twitter.com/mgedmin) created a little [bash script](https://github.com/mgedmin/scripts/blob/master/list-obsolete-packages)
which lists unavailable (+-=unsupported) packages...
```
apt-show-versions |grep "No available version in archive"|cut -f 1 -d ' '|sort
```

## sources

- [packages in main are supported for five years](https://lists.ubuntu.com/archives/ubuntu-devel-discuss/2016-April/016485.html)
- [Die LTS Frage](https://kofler.info/die-lts-frage/) - German only
