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
  
        Codigo para generar la tabla de SubCategorias
  <pre><code> 
    list_sub_category = products['sub_category'].unique()
    size_sub_category = len(list_sub_category)
    list_id_sub_category = list(range(1,size_sub_category+1))
    sub_category = pd.DataFrame({'id_sub_category': list_id_sub_category,
                            'name_sub_category': list_sub_category})
                        </code></pre>
- Productos
  
        Codigo para generar la tabla de Productos
  <pre><code> 
    products_value_counts = products['items'].value_counts().reset_index()
    products_value_counts = products_value_counts.rename(columns={'items': 'count', 'index': 'items'})
    products = pd.merge(products, products_value_counts, on='items', how='left')
    products = products.query('count == 1.0')
    size_products = len(products)
    list_id_products = list(range(1,size_products+1))
    products = products.assign(id_product=list_id_products)
    products = pd.merge(products, category, left_on='category', right_on='name_category', how='left')
    products = pd.merge(products, sub_category, left_on='sub_category', right_on='name_sub_category', how='left')
    products =products.rename(columns={'items': 'name_product'})
    products = products[['id_product', 'name_product', 'href', 'price', 'id_category', 'id_sub_category']]
                        </code></pre>