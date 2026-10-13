# Wisemusic OS

Plugin Wisemusic pro Claude. Přináší firemní konektor (Wisemusic OS) a 25 dovedností týmu do chatu Claude,
do Coworku a do Claude Code.

## Jak začít

1. Otevřete v pluginu záložku **Connectors** a připojte **wisemusic-os**. Přihlaste se svým účtem Wisemusic;
   přístup potvrzujete jen jednou.
2. Ptejte se Clauda na cokoli ve firmě Wisemusic, třeba „co se děje s …?“. Claude odpovídá z firemního modelu,
   znalostní báze a schůzek, se zdroji, a ukáže jen to, co smí vidět vaše role.
3. Začněte dovedností „start here“ svého týmu. Změny se vždy jen navrhují; každou schválí člověk.

## Data

Konektor posílá vaše dotazy a volání nástrojů, která Claude dělá, na vlastní bránu Wisemusic na mcp.wisemusic.vono.studio,
přihlášený jako vy. Každé volání se ověří podle vaší role a zapíše do auditního logu firmy. Plugin sám
nic neukládá a neobsahuje žádné klíče ani hesla.

## Instalace

* Claude Code: `/plugin install wisemusic-os --marketplace jstudnic1/wisemusic-claude-plugins`
* claude.ai a Cowork: **Customize > Plugins > Add > Add marketplace** s adresou `https://github.com/jstudnic1/wisemusic-claude-plugins`,
  pak nainstalujte wisemusic-os a připojte ho na záložce **Connectors**. Vlastník organizace ho může přidat všem
  v **Organization settings > Plugins & skills**.
