<script>
	let empleados=[];
	let datosEmpleado={
		id:null,
		nombre:"",
		correo:""
	}

	let mostrarEmpleados=()=>{
		fetch('http://localhost/empleados/')
		.then(respuesta=>respuesta.json())
		.then((datosRespuesta)=>{
			empleados=datosRespuesta;
			datosEmpleado={
				id:null,
				nombre:"",
				correo:""
			}
			console.log(empleados);
		}).catch(console.log)
	}
	let agregarEmpleado = ()=>{
	const nuevoEmpleado={
		id:datosEmpleado.idEmpleado,
		nombre:datosEmpleado.nombre,
		correo:datosEmpleado.nombre
	}

	fetch('http://localhost/empleados/?insertar=1',{ 
	method:"POST",
	body:JSON.stringify(nuevoEmpleado)
	})
		.then(respuesta=>respuesta.json())
		.then((datosRespuesta)=>{
			mostrarEmpleados();
			console.log(empleados);
		}).catch(console.log)
	}
	let borrarEmpleado =idEmpleado =>{
		fetch('http://localhost/empleados/?borrar='+idEmpleado)
            .then(respuesta=>respuesta.json())
            .then((datosRespuesta)=>{
               mostrarEmpleados();
            })
            .catch(console.log)     
	}
	let editarEmpleado = empleado => {
		datosEmpleado = empleado;
	}
	let actualizarEmpleado = () =>{
		fetch('http://localhost/empleados/?actualizar='+datosEmpleado.idEmpleado,{ 
		method:"POST",
		body:JSON.stringify(datosEmpleado)
		})
			.then(respuesta=>respuesta.json())
			.then((datosRespuesta)=>{
				console.log(datosRespuesta);
				mostrarEmpleados();
			}).catch(console.log)
	}

	mostrarEmpleados();

</script>
<div class="container">
	<div class="row">
		<div class="col-md-6">
			<div class="card">
				<div class="card-header">
					Beneficiarios  
				</div>
				<div class="card-body">
					<form>
						<div class="mb-3">
						<label for="" class="form-label">ID</label>
						<input bind:value={datosEmpleado.idEmpleado}
						type="text" class="form-control" name="" id="" aria-describedby="helpId" readonly>
						</div>
						<div class="mb-3">
						<label for="" class="form-label">Nombre</label>
						<input bind:value={datosEmpleado.nombre}
						type="text" class="form-control" name="" id="" aria-describedby="helpId" placeholder="">
						</div>
						<div class="mb-3">
						<label for="" class="form-label">Correo</label>
						<input bind:value={datosEmpleado.correo}
						type="email" class="form-control" name="" id="" aria-describedby="helpId" placeholder="">
						</div>
						<button type=button class="btn btn-primary" href="" on:click|preventDefault={agregarEmpleado}>Añadir</button>
						<button type=button class="btn btn-warning" href="" on:click|preventDefault={actualizarEmpleado}>Actualizar</button>
					</form>
				</div>
			</div>
		</div>
		<div class="col-md-6">
			<div class="card">
				<div class="card-body">
					<div class="table">
						<table class="table">
							<thead>
								<tr>
									<th scope="col">ID</th>
									<th scope="col">Nombre</th>
									<th scope="col">Correo</th>
									<th scope="col">Acciones</th>
								</tr>
							</thead>
							<tbody>
								{#each empleados as empleado}
									<tr class="">
										<td>{empleado.idEmpleado}</td>
										<td>{empleado.nombre}</td>
										<td>{empleado.correo}</td>
										<td>
											<button
											type="submit"
											class="btn btn-link"
											on:click={editarEmpleado(empleado)}>
												Editar
											</button> | 
											<button
											type="submit"
											class="btn btn-link"
											on:click={borrarEmpleado(empleado.idEmpleado)}>
												Eliminar
											</button>
										</td>
									</tr>
								{/each}
							</tbody>
						</table>
					</div>
				</div>
			</div>
		</div>
		
	</div>
</div>
