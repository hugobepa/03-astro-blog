(relleno de pagina)[https://gist.github.com/Klerith/01bd995e401d5bb6d8d449d0599b1c3d]

0. creamos pagina y la llenamos `src\pages\blog\[page].astro`:
   - funcion trabajar param estaticos`import type { GetStaticPaths } from "astro";` : `export const getStaticPaths`
     - lo pasamos a async y obtenemos la paginacion : `async ({paginate})`
     - obtenemos los datos de los blogs: `const blogPosts = await getCollection('blog');`
     - enviamos los datos obtenidos y 2 elementos por pagina : `blogPosts,{pageSize: 2`
   - Declarariamos la propiedad `page` para poder trabajar: `const { page } = Astro.props;`
   - obtenenemos los datos de los `posts` mediante `page` y los pasamsoa al componente:
     `  {page.data.map((post) => <TypedBlogPost post={post} />)}`
   - pasamos los datos `page` para pasar las paginas `page.url.prev`.

- fichero:

```
---
import type { GetStaticPaths } from "astro";
  // Type GetStaticPaths de Astro
import TypedBlogPost from '@components/TypedBlogPost.astro';
import MainLayout from '../../layouts/MainLayout.astro';
import { getCollection } from "astro:content";

export const getStaticPaths = ( async ({paginate})=> {

    const blogPosts = await getCollection('blog');

    return paginate(blogPosts,{pageSize: 2});
}) satisfies GetStaticPaths;

const { page } = Astro.props;
---


  {page.data.map((post) => <TypedBlogPost post={post} />)}


   <a href={page.url.prev}

    <a href={page.url.next}
```
