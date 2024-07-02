<script>
 
 let products = [
	{
		id: 1,
		name: 'HP Notebook',
		description:'HP Laptop',
		category: 'laptop'
	},
	{
		id: 2,
		name: 'HP Notebook',
		description:'HP Laptop',
		category: 'laptop'
	},
 ];

	let product = {
		id: "",
		name: "",
		description: "",
		category: "",
		imageURL: ""
	};

	let editStatus = false;

	const cleanProduct = () => {
		product ={
			id:'',
			name:'',
			description:'',
			category:'',
			imageURL:''
		}
	}

	const addProduct = () => {		
		const newProduct ={
			id: products.length + 1,
			name: product.name,
			description: product.description,
			category: product.category,
			imageURL: product.imageURL
		}
		products = products.concat(newProduct)
		cleanProduct();
		console.log(products)
	}

	const updateProduct = () => {
		let updatedProduct = {
			name: product.name,
			description: product.description,
			id: product.id,
			imageURL: product.imageURL,
			category: product.category
		}
		const productIndex = products.findIndex(p => p.id === product.id)
		products[productIndex] = updatedProduct;
		cleanProduct();
		editStatus = false;
	}

	const onSubmitHandler = e => {
		if (!editStatus){
		addProduct();
		} else {
			updateProduct();
		}
	};

	const deleteProduct = (id) =>{
		products= products.filter(product => product.id !== id);
	}

	const editProduct = productEdited => {
		product = productEdited;
		editStatus = true;
	}

</script>

<main>
 <div class="container p-4">
	<class class="row">

		<div class="col-md-6">
			<div class="card">
				<div class="card-body">
					<form on:submit|preventDefault={onSubmitHandler}>
						<div class="form-group">
							<input bind:value={product.name} type="text" placeholder="Product name" id="product-name" class="form-control" />
						</div>
						
						<div class="form-group">
						  <textarea
						  bind:value={product.description}
						  id="product-description"
						  rows="3"
						  placeholder="Product Description" class="form-control"></textarea>
						</div>
					
						<div class="form-group">
						  <input
						  bind:value={product.imageURL}
						  type="url"
						  id="product-image-url"
						  placeholder="https://faztweb.com/"
						  class="form-control"/>
						</div>

						<div class="form-group">
							<select id="category" bind:value={product.category} class="form-control">
								<option value="laptops">Laptops</option>
								<option value="peripherials">Periféricos</option>
								<option value="Servers">Servidores</option>
							</select>
						</div>
						
						<button class="btn btn-primary">
						{#if !editStatus}Guardar producto {:else}Actualizar Producto{/if}
						</button>  
					</form>
				</div>
			</div>
		</div>
		<div class="col-md-6">
			{#each products as product}
			<div class="card mt-2">
				<div class="row">
					<div class="col-md-4">
						{#if !product.imageURL}
						<img src="images/no_products_found.jpg" alt="" class="img-fluid p-2">
						{:else}
						<img src="{product.imageURL}" alt="" class="img-fluid p-2">
						{/if}
					</div>
					<div class="col-md-8">
						<div class="card-body">
							<h5>
								<strong>{product.name}</strong>
								<span>
									<small>{product.category}</small>	
								</span>	
								</h5>
								<p class="card-text">{product.description}</p>
								<button class="btn btn-danger" on:click={deleteProduct(product.id)}>
									Borrar
								</button>
								<button class="btn btn-secondary" on:click={editProduct(product)}>
									Editar
								</button>
						</div>
					</div>
				</div>

			</div>
			{/each}
		</div>
		
	
	</class>
 </div>

</main>

<style>
</style>
