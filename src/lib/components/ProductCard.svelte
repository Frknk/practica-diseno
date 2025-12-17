<script lang="ts">
  import { Badge } from "$lib/components/ui/badge";
  import { Button } from "$lib/components/ui/button";
  import { Card, CardContent, CardFooter, CardHeader } from "$lib/components/ui/card";
  import { Image, Star } from "lucide-svelte";

  let { title, type, badge, imageColor = "bg-gray-200", rating = 4.5 } = $props();
</script>

<Card class="overflow-hidden border-0 shadow-none">
  <CardHeader class="p-0">
    <div class={`aspect-square w-full ${imageColor} flex items-center justify-center relative rounded-xl`}>
      <div class="absolute top-3 left-3 flex items-center gap-1 bg-white/90 backdrop-blur-sm px-2 py-1 rounded-md shadow-sm">
        <Star class="size-3.5 fill-yellow-400 text-yellow-400" />
        <span class="text-xs font-semibold">{rating}</span>
      </div>
      {#if badge}
        <Badge class="absolute top-3 right-3 bg-white text-black hover:bg-white/90 shadow-sm">{badge}</Badge>
      {/if}
      <Image class="size-12 text-gray-400" />
    </div>
  </CardHeader>
  <CardContent class="p-4 text-center">
    <h3 class="font-semibold text-lg">{title}</h3>
    <p class="text-muted-foreground text-sm">{type}</p>
  </CardContent>
  <CardFooter class="p-4 pt-0 flex justify-center">
    <a href="/product"><Button variant="outline" class="rounded-full px-8 border-gray-300 hover:bg-gray-100 hover:text-black">Comprar</Button></a>
  </CardFooter>
</Card>
