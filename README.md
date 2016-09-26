# JSONB_query_sample


## LIKE
      SELECT *  FROM INVOICE ,jsonb_array_elements(content->'invoiceLines') AS "content.invoiceLines[]"
      WHERE   "content.invoiceLines[]"->'tax'->>'code' LIKE 'D%'



## EQUALS
      SELECT "content.invoiceLines[]"->'tax' FROM ( SELECT * FROM INVOICE WHERE content->'invoiceLines' @> cast
      ('[{"tax":{"id":"'||(:contentinvoiceLinestaxid)||'"}}]' as jsonb) ) AS "INVOICE",
        jsonb_array_elements(content->'invoiceLines') AS "content.invoiceLines[]"
      WHERE "content.invoiceLines[]"->'tax' @> cast('{"id":"'||(:contentinvoiceLinestaxid)||'"}' as jsonb)
