<script lang="ts">
  import { Button } from "$lib/components/ui/button";
  import { Input } from "$lib/components/ui/input";
  import { Search } from "lucide-svelte";
</script>

<header class="border-b py-4">
  <div class="container mx-auto flex items-center justify-between px-4">
    <!-- Logo -->
    <div class="flex items-center gap-2">
      <a href="/"><h1 class="text-3xl font-bold tracking-tight">UtilesGo</h1></a>
    </div>

    <!-- Navigation -->
    <nav class="hidden md:flex items-center gap-6 text-lg font-medium">
      <a href="/" class="hover:text-primary transition-colors">Inicio</a>
      <a href="/productos" class="hover:text-primary transition-colors">Productos</a>
      <a href="/busqueda" class="hover:text-primary transition-colors">Busqueda Avanzada</a>
    </nav>

    <!-- Actions -->
    <div class="flex items-center gap-4">
      <div class="relative w-full max-w-sm items-center hidden sm:flex">
        <Input type="search" placeholder="Value" class="pr-10 rounded-full" />
        <span class="absolute right-0 inset-y-0 flex items-center justify-center px-3">
          <Search class="size-4 text-muted-foreground" />
        </span>
      </div>
      <a href="/login"><Button variant="default" class="bg-gray-900 text-white hover:bg-gray-800">Login</Button></a>
    </div>
  </div>
</header>
