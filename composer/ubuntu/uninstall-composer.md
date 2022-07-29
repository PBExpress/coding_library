# Uninstall Composer

**Uninstall composer**

To remove just composer package itself from Ubuntu execute on terminal:

```
sudo apt-get remove composer
```

**Uninstall composer and it's dependent packages**

To remove the composer package and any other dependant package which are no longer needed from Ubuntu Xenial.

```
sudo apt-get remove --auto-remove composer
```

**Purging composer**

If you also want to delete configuration and/or data files of composer from Ubuntu Xenial then this will work:

```
sudo apt-get purge composer
```

To delete configuration and/or data files of composer and it's dependencies from Ubuntu Xenial then execute:

```
sudo apt-get purge --auto-remove composer
```
