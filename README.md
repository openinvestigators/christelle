# False Evidence in Tariq Ramadan Court Case

In a previous repository, we have already [demonstrated](https://github.com/openinvestigators/tariq-twitter), how Tariq Ramadan is inflating his Twitter following with fake followers. Today we are looking at allegations of hate speech around Mr. Ramadan's ongoing trial, of which one of his victims (pseudonym "Christelle") is accused of.

A previous journalist – Mathieu VERNEREY – has written a [lengthy blog post](https://mathieuvernerey.wordpress.com/2020/07/03/autoreflexion-blog-antisemite-extreme-droite/) that implicates Christelle with hate speech posted on various blogs and social media accounts. The post is very long, but luckily Mr. Vernerey made a crucial mistake in the first part, so everything that follows can be ignored.

In detail, Mr. Vernerey links an archived blog, previously hosted on `blog.ifrance.com` to the victim's full name because it appears in the URL. On this blog the authors announces the migration to the hate speech-filled blog on `autoreflexion.wordpress.com`.

> Reroutage du blog

> Publié le 03 juin 2010 à 00:21

> Par emma

> Parce que les blogs ifrance s’affichent mal ou pas du tout pendant plusieurs jours, parce que semble-t-il Ifrance est en passe de fermeture, parce que toutes les 3 nous ne souhaitons plus nous limiter au secteur de la protection animale… continuez la lecture a cette adresse : http://autoreflexion.wordpress.com/category/veganismeantispecisme-environnement-protection-animale/

Sadly it's more complicated than just finding this announcement. Upon closer examination it seems the wayback machine snapshots of the cited blog `blog.ifrance.com/paule-emmaaline` have technical issues and every snapshot copied the content of another site. So the URL can't be linked to the content in a reliable way. Here a selection of blogs copied to the said URL:

- "Le Journanal du Markus" https://web.archive.org/web/20110220000939/http://blog.ifrance.com/paule-emmaaline > http://markus.leicht.free.fr/phpbb3/
- "Le Blog de FrAnKkApS" https://web.archive.org/web/20100609141007/http://blog.ifrance.com:80/paule-emmaaline > http://frankkaps.free.fr/index2.html
- "Le blog de dofus-p249" https://web.archive.org/web/20100519055806/http://blog.ifrance.com:80/paule-emmaaline > ??
- "CAMBROUSSE ROCK": https://web.archive.org/web/20100501090113/http://blog.ifrance.com:80/paule-emmaaline > cambrousserock@hotmail.fr
- "Johnny Hallyday - Bienvenue chez Johnny" https://web.archive.org/web/20100113101032/http://blog.ifrance.com:80/paule-emmaaline > http://blog.ifrance.com/passion41
- "BORINAQUA école de plongée" https://web.archive.org/web/20100109005536/http://blog.ifrance.com:80/paule-emmaaline > http://blog.ifrance.com/borinaqua

All those blogs seem to be hosted under the same site `blog.ifrance.com/paule-emmaaline` according to Wayback machine. It should be clear that those blogs are unrelated with each other and especially the author's name given in the URL path.

To be sure, we downloaded *every site* archived under this URL prefix. To achieve this, you can use a simple [Ruby script](https://github.com/hartator/wayback-machine-downloader):

```
$ wayback_machine_downloader -s http://blog.ifrance.com/paule-emmaaline
```

In total we were able to download about 1400 pages archived under this blog. The CSS and HTML of most pages is broken, so one needs to look at the source code for the actual content. In this case we are only interested in the page titles. You can use `grep` or the [Silver Searcher](https://github.com/ggreer/the_silver_searcher) to find the title line for each file.

```
$ ag --nofilename '<title>' > title-matches.txt
```

This yields a list of titles, like below:

```html
<title>aide - Blog games-network </title>
<title>Les archives par jour - 26/07/2007 - Les Animaux font leur blog</title>
<title>Les archives par mois - 07/2006 - OUKHIT BLAD LKHIR</title>
<title>Les Animaux font leur blog</title>
<title>Les religions et le porc : l'histoire et les textes saints- Les Animaux font leur blog</title>
<title>Les archives par mois - 06/2008 - Le Blog de FrAnKkApS</title>
<title>Les archives par mois - 06/2009 - Le Blog de FrAnKkApS</title>
<title>geocompteur - Les Animaux font leur blog</title>
```

About half the entries are by a blog titled "Les Animaux font leur blog". The rest are from other sites. There are certainly more things that could be done with this dump of HTML documents. E.g. find common footers or author names. It should still be clear that Internet Archive's Wayback machine messed up in this case and the content from all those random blogs can't be associated with a blog or user `paule-emmaaline`.