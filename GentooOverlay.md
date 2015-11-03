#summary Howto add tryton overlay for Gentoo.
#labels Phase-Deploy

## Add tryton to [layman](http://layman.sourceforge.net/) local overlays list ##
```
layman -a tryton
```

## Synchronize tryton overlay ##
```
layman -s tryton
```

Now you can use emerge to install tryton