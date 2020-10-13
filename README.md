# MCOC2020-P2
MCOC2020-P2 

Para el rediseño se escogieron las barras 0, 1, 2, 28 y 29

La función de rediseño de cada barra es la siguiente:
```
def rediseñar(self, Fu, ϕ=0.9):
		"""Para la fuerza Fu (proveniente de una combinacion de cargas)
		re-calcular el radio y el espesor de la barra de modo que
		se cumplan las disposiciones de diseño lo más cerca posible
		a FU = 1.0.
		"""
		f = 1.
		p = 1e-4

		while f > 0:

			self.R = self.R * f
			self.t = self.t * f	

			if self.obtener_factor_utilizacion(Fu, ϕ=0.9) < 0.99:
				self.R = self.R / f
				self.t = self.t / f	
				f = f - p

			elif self.obtener_factor_utilizacion(Fu, ϕ=0.9) > 1.:
				self.R = self.R / f
				self.t = self.t / f	

				f = f + p

				self.R = self.R * f
				self.t = self.t * f
				break

			else:
				break

		"""Aqui se cambia R y t para que tengan un valor entero"""

		R = ceil(self.R * 100)
		t = ceil(self.t * 1000)

		self.R = R/100
		self.t = t/1000

		return self.R, self.t
```

Donde inicialmente se determina el valor de el factor de amplificación "f" y el paso "p". "p" comienza a modificar el valor de "f" dependiendo de el nuevo valor del factor de utilización "FU", es decir, si FU es menor a 1 entonces "f" continua disminuyendo hasta que supera el FU = 1.0. Finalmente, una vez que FU está lo más cercano a 1.0, se ajusta el valor de "R" y "t" de la barra, de modo que sean valores enteros, por ejemplo 2.3 cm = 3.0 cm.
