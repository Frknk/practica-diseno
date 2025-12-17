<script lang="ts">
  import Header from "$lib/components/Header.svelte";
  import ProductCard from "$lib/components/ProductCard.svelte";

  const products = [
    { title: "Mochila Escolar", type: "Mochilas", badge: "Nuevo", imageColor: "bg-blue-100", rating: 4.8 },
    { title: "Set de Lápices", type: "Lápices", badge: "Oferta", imageColor: "bg-yellow-100", rating: 4.5 },
    { title: "Cuaderno A4", type: "Cuadernos", badge: "Nuevo", imageColor: "bg-green-100", rating: 4.2 },
    { title: "Estuche Grande", type: "Estuches", badge: "Nuevo", imageColor: "bg-purple-100", rating: 4.9 },
    { title: "Regla 30cm", type: "Reglas", badge: "Viejo", imageColor: "bg-red-100", rating: 4.0 },
    { title: "Borrador", type: "Borradores", badge: "Nuevo", imageColor: "bg-gray-100", rating: 4.3 },
    { title: "Tijeras", type: "Tijeras", badge: "Oferta", imageColor: "bg-orange-100", rating: 4.6 },
    { title: "Pegamento", type: "Pegamentos", badge: "Nuevo", imageColor: "bg-teal-100", rating: 4.1 },
  ];
</script>

<div class="min-h-screen bg-white font-sans">
  <Header />

  <main class="container mx-auto px-4 py-12">
    <div class="mb-10 text-center">
      <h2 class="text-3xl font-bold tracking-tight mb-2">Productos Destacados</h2>
      <p class="text-muted-foreground">Encuentra los mejores útiles para tu regreso a clases</p>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-8">
      {#each products as product}
        <ProductCard 
          title={product.title} 
          type={product.type} 
          badge={product.badge} 
          imageColor={product.imageColor} 
          rating={product.rating}
        />
      {/each}
    </div>
  </main>
</div>
