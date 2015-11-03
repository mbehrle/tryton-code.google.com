# Migration from 2.8 -> 3.0 #

## Must ##

  * Run this SQL query: `DELETE FROM ir_translation WHERE id IN (SELECT MAX(id) FROM ir_translation GROUP BY name, res_id, lang, type, src_md5, module HAVING COUNT(1) > 1);`
  * If `project_revenue` is installed `timesheet_cost` must be installed on update with `-i timesheet_cost`.