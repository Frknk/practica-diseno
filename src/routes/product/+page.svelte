<script lang="ts">
  import Header from "$lib/components/Header.svelte";
  import { Button } from "$lib/components/ui/button";
  import { Card, CardContent, CardHeader, CardTitle } from "$lib/components/ui/card";
  import { Input } from "$lib/components/ui/input";
  import { User, Check, Send, Smile, Mic, Clock, MessageCircle } from "lucide-svelte";
</script>

<div class="min-h-screen bg-white font-sans">
  <Header />

  <main class="container mx-auto px-4 py-8">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8 items-start">
      
      <!-- Left Column: Product Image & Actions -->
      <div class="flex flex-col gap-6 min-w-0 border-2 border-neutral-950 p-6 bg-white">
        <div class="border-2 border-neutral-950 bg-white">
          <div class="aspect-square bg-gray-50 flex items-center justify-center relative border-b-2 border-neutral-950">
            <!-- Placeholder X -->
            <div class="absolute inset-0 flex items-center justify-center">
                <div class="w-full h-px bg-gray-300 rotate-45 absolute"></div>
                <div class="w-full h-px bg-gray-300 -rotate-45 absolute"></div>
            </div>
          </div>
          <div class="p-4 text-center bg-white">
            <h2 class="text-2xl font-bold uppercase tracking-wider">Intercambio</h2>
          </div>
        </div>

        <div class="space-y-4 border-2 border-neutral-950 p-4 bg-white">
          <h3 class="font-medium">Tipo de contactos</h3>
          <div class="flex gap-8 flex-wrap">
            <div class="flex items-center space-x-2">
                <MessageCircle />
            </div>
            <div class="flex items-center space-x-2">
                <MessageCircle />
            </div>
            <div class="flex items-center space-x-2">
                <MessageCircle />
            </div>
          </div>
        </div>

        <div class="border-2 border-neutral-950 bg-white">
          <Button class="w-full h-12 text-lg border-0 rounded-none bg-white text-black hover:bg-gray-100" variant="outline">
            Iniciar chat en linea
          </Button>
        </div>
      </div>

      <!-- Middle Column: Details -->
      <div class="flex flex-col gap-6 min-w-0 border-2 border-neutral-950 p-6 bg-white">
        <Card class="border-2 border-neutral-950 rounded-none shadow-none bg-white">
          <CardHeader>
            <CardTitle class="text-2xl font-bold">Detalles</CardTitle>
          </CardHeader>
          <CardContent class="space-y-4 text-lg">
            <p>Camisa color blanco</p>
            <p><span class="font-semibold">Marca:</span> Gucci</p>
            <p><span class="font-semibold">Talla:</span> S</p>
            <p><span class="font-semibold">Motivo:</span> No dicho</p>
            <p class="pt-4">Usuario publicador</p>
          </CardContent>
        </Card>

        <Card class="border-2 border-neutral-950 rounded-none shadow-none p-4 flex items-center gap-4 bg-white">
            <div class="h-10 w-10 rounded-full border-2 border-neutral-950 flex items-center justify-center shrink-0">
                <User class="h-6 w-6" />
            </div>
            <span class="text-xl font-bold truncate">Fred Polinar</span>
        </Card>

        <div class="border-2 border-neutral-950 h-48 relative bg-gray-50">
             <div class="absolute inset-0 flex items-center justify-center">
                <div class="w-full h-px bg-gray-300 rotate-45 absolute"></div>
                <div class="w-full h-px bg-gray-300 -rotate-45 absolute"></div>
            </div>
        </div>
      </div>

      <!-- Right Column: Chat -->
      <div class="border-2 border-neutral-950 flex flex-col h-[800px] min-w-0 bg-white p-4 gap-4">
        <!-- Chat Header -->
        <div class="border-2 border-neutral-950 p-3 flex items-center justify-between text-sm font-medium bg-white">
            <div class="flex items-center gap-4">
                <div class="flex items-center gap-1">
                    <Clock class="h-4 w-4" />
                    <span>20 Minutos</span>
                </div>
                <div class="h-4 w-px bg-neutral-950"></div>
                <span>Chat Seguro</span>
            </div>
            <div class="flex items-center gap-2">
                <span>En linea</span>
                <div class="h-3 w-3 rounded-full bg-green-500 border border-neutral-950"></div>
            </div>
        </div>

        <!-- Chat Messages -->
        <div class="flex-1 p-4 space-y-8 overflow-y-auto border-2 border-neutral-950 bg-white">
            <!-- Message 1 -->
            <div class="space-y-2">
                <div class="flex items-center gap-2">
                    <User class="h-5 w-5" />
                    <span class="font-bold text-lg">Fred Polinar</span>
                    <div class="border border-neutral-950 p-0.5 rounded">
                        <Check class="h-3 w-3" />
                    </div>
                </div>
                <div class="border-2 border-neutral-950 p-4 bg-white">
                    <p class="text-gray-400 italic text-sm">
                        mmmmm mmmm mmm mmm mmmm<br>
                        mmmmmmmmm mmmmmmmm<br>
                        mmm mm m mmmm mmmmmm<br>
                        mmmmm m mmmm m<br>
                        mmm mm mmmm m<br>
                        mm m mmm mmm mm
                    </p>
                </div>
            </div>

            <!-- Message 2 -->
            <div class="space-y-2">
                <div class="flex items-center gap-2 justify-end">
                    <User class="h-5 w-5" />
                    <span class="font-bold text-lg">Tevis Acharte</span>
                </div>
                <div class="border-2 border-neutral-950 p-4 bg-white">
                    <p class="text-gray-400 italic text-sm text-right">
                        mm mmm mmm uns mm<br>
                        mmmmmmm mmmmmmm<br>
                        mmm mm m mmmm mmmm<br>
                        mmmmm m mmmm m<br>
                        mmm mm mmmm m<br>
                        mm m mmm mmm mm
                    </p>
                </div>
            </div>
        </div>

        <!-- Chat Footer -->
        <div class="p-4 border-2 border-neutral-950 space-y-2 bg-white">
            <div class="flex items-center justify-center gap-2 text-xs font-medium">
                <span>Este chat es seguro y no se compartira</span>
                <Mic class="h-4 w-4" />
            </div>
            <div class="relative">
                <Input class="border-2 border-neutral-950 rounded-none h-12 pr-20" placeholder="" />
                <div class="absolute right-2 top-1/2 -translate-y-1/2 flex items-center gap-2">
                    <Button variant="ghost" size="icon" class="h-8 w-8">
                        <Smile class="h-5 w-5" />
                    </Button>
                    <Button variant="ghost" size="icon" class="h-8 w-8">
                        <div class="rounded-full border-2 border-neutral-950 p-1">
                            <Send class="h-3 w-3" />
                        </div>
                    </Button>
                </div>
            </div>
        </div>
      </div>

    </div>
  </main>
</div>
