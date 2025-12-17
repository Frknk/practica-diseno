<script lang="ts">
	import Header from "$lib/components/Header.svelte";
	import { Button } from "$lib/components/ui/button/index.js";
	import { Input } from "$lib/components/ui/input/index.js";
	import * as Card from "$lib/components/ui/card/index.js";
	import { Image } from "lucide-svelte";
</script>

<div class="min-h-screen bg-white font-sans flex flex-col">
	<Header />

	<main class="flex-1 container mx-auto px-4 py-12 flex items-center justify-center">
		<div class="w-full max-w-6xl grid grid-cols-1 md:grid-cols-2 gap-12 items-center">
			<!-- Left Column: Marketplace Image Placeholder -->
			<div class="hidden md:flex flex-col gap-4">
				<h2 class="text-3xl font-bold tracking-tight text-center md:text-left">Marketplace</h2>
				<div class="aspect-square bg-gray-200 rounded-lg flex items-center justify-center">
					<Image class="w-32 h-32 text-gray-300" />
				</div>
			</div>

			<!-- Right Column: Login Form -->
			<div class="flex flex-col items-center justify-center w-full max-w-md mx-auto">
				<div class="text-center mb-8">
					<h1 class="text-4xl font-bold mb-2">UtilesGo</h1>
					<p class="text-xl text-muted-foreground">Inicio de Sesión</p>
				</div>

				<Card.Root class="w-full border-none shadow-none">
					<Card.Content class="space-y-6 p-0">
						<div class="space-y-2">
							<label for="email" class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70">
								Correo institucional
							</label>
							<Input id="email" type="email" placeholder="Value" />
						</div>
						
						<div class="space-y-2">
							<label for="password" class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70">
								Contraseña
							</label>
							<Input id="password" type="password" placeholder="Value" />
						</div>

						<Button class="w-full bg-neutral-800 hover:bg-neutral-900 text-white" size="lg">
							Inicio de Sesión
						</Button>
					</Card.Content>
					
					<Card.Footer class="flex justify-center p-0 mt-6">
						<p class="text-sm text-muted-foreground">
							No tienes cuenta? 
							<a href="/register" class="underline underline-offset-4 hover:text-primary">
								Click Aqui
							</a>
						</p>
					</Card.Footer>
				</Card.Root>
			</div>
		</div>
	</main>
</div>
