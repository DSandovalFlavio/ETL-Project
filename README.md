# ETL Project
Proyecto de migracion de sistema crm a base de datos postgresql para disponibilizar la data

Se utilizara:

- Python
- Pandas
- SQLAlchemy
- PostgreSQL

Pasos a seguir:

Generar tablas de: 

- Categorias

        Codigo para generar la tabla de Categorias
  <pre><code> 
    list_category = products['category'].unique()
    size_category = len(list_category)
    list_id_category = list(range(1,size_category+1))
    category = pd.DataFrame({'category_name': list_category,
                        'category_id': list_id_category})
                        </code></pre>

- Subcategorias 
- Productos
