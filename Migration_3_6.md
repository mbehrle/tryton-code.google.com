# Migration from 3.4 -> 3.6 #

## MUST ##

  * `[XML]` Use `width`/`height` instead of `img_width`/`img_height`
  * `[PY]` New API for on\_change: the instance is modified instead of returning a dictionary.
    * Example: http://hg.tryton.org/modules/party/rev/3be0dbb6bf94
  * `[SQL]`: Fix amount second currency with:
> > ` UPDATE account_move_line SET amount_second_currency = (amount_second_currency * -1) WHERE amount_second_currency IS NOT NULL AND SIGN(amount_second_currency) != SIGN(debit - credit); `
  * `[PY]`: Replace `float_time` widget by `TimeDelta` field.
  * `[XML]`: Use `pyson` for fields that where evalueted using safe\_eval. Example: http://hg.tryton.org/modules/account/rev/d60176cc48a2
  * `[XML]`: There is no more a datetime widget for list/tree, two columns with one widget date and one widget time should be used instead. Example: http://hg.tryton.org/trytond/rev/4a2d1a76de52
  * `[PY]`: The API of the Report class has been reworked to improve the customization of the engine. The formatting methods are now more strict to prevent silent failure.

## NEW ##

  * `[PY]`: `save` could be used as a class method too
    * Example: http://hg.tryton.org/modules/stock/rev/4f346cd0dd23
  * `[PY]`: `restore_history_before` class method added
  * `[PY]`: `ModuleTestCase` is added so it's simplier to implement modules test cases. Example: http://hg.tryton.org/modules/account/rev/f9840513b549