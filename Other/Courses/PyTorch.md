---
Resources:
  - https://github.com/yunjey/pytorch-tutorial
  - https://github.com/ritchieng/the-incredible-pytorch
---
### PyTorch for Deep Learning
By freeCodeCamp: 
![PyTorch for Deep Learning](https://www.youtube.com/watch?v=GIsg-ZUy0MY)
*See description for notebooks on Jovian*
##### Summary
###### 01- PyTorch basics
- Tensors and tensor operations
	- Addition & multiplication
	- Gradient/derivatives computation
		```python
		# Create tensors.
		x = torch.tensor(3.)
		w = torch.tensor(4., requires_grad=True)
		b = torch.tensor(5., requires_grad=True)
		
		y = w * x + b
		
		# Compute derivatives
		y.backward()
		
		# Derivatives are then stored in the grad attribute of the tensors
		print('dy/dx:', x.grad)
		print('dy/dw:', w.grad)
		print('dy/db:', b.grad)
		
		# dy/dx: None (requires_grad attr False)
		# dy/dw: tensor(3.) 
		# dy/db: tensor(1.)
		```
- Interoperability with Numpy
	```python
	# Numpy -> Torch
	y_torch = torch.from_numpy(x_np)

	# Torch -> Numpy
	x_np = y.numpy()
	```
- Other operations
	```python
	# Random tensors
	w = torch.randn(2, 3, requires_grad=True) # 2 rows, 3 cols
	b = torch.randn(2, requires_grad=True) 
	# Generates random vectors from standard normal distribution

	# Tensor sum
	torch.sum(t1, t2)

	# Number of elements
	t1.numel()
	
	# Tensor transpose
	transpose = w.t()

	# Matrix multiplication
	mul = x @ w
	```
###### 02- Gradient Descent and Linear Regression with PyTorch
- TensorDataset & DataLoader
	```python
	from torch.utils.data import TensorDataset
	from torch.utils.data import DataLoader 
	```
	- **TensorDataset** allows for the manipulation of the data (inputs and targets): slicing and splitting into training and testing sets
	- **DataLoader** is useful to load batches of predefined sizes during training epochs, it also allows for shuffling utilities
		>[!info]- Analogy
		>" *TensorDataset is to Pytorch what Dataframe is to Pandas* " 
- The '**torch.nn**' module
> **Model**  
> ```python
> model = nn.Linear(input_features, output, bias=boolean)
>
>model.parameters() # returns a list of the weights and biases of the model
 ># Example: [Parameter containing:
 ># tensor([[ 0.1304, -0.1898,  0.2187],
 >#     [ 0.2360,  0.4139, -0.4540]], requires_grad=True),
 > # Parameter containing:
 > # tensor([0.3457, 0.3883], requires_grad=True)]
> ```
> **Loss function**  
> ``` python
> from torch.nn.functional import F 
> mse_fn = F.mse_loss
> loss = mse_fn(model(inputs), targets)
> ```
> **Optimiser**
>  ``` python
 >opt = torch.optim.SGD(model.parameters(), lr=1e-5)
 >opt.step() # updates the parameters
 >```

>[!warning]- About reseting gradients
>At the end of a training epoch, always remember to set gradients back to zero using `opt.zero_grad()` otherwise PyTorch will accumulate the gradients over epochs resulting in unwanted results 
- Simple fitting loop: Linear regression
	```python
	# Utility function to train the model
	def fit(num_epochs, model, loss_fn, opt, train_dl):
		
		# Repeat for given number of epochs
		for epoch in range(num_epochs):
			
			# Train with batches of data
			for xb,yb in train_dl:
				
				# 1. Generate predictions
				pred = model(xb)
				# 2. Calculate loss
				loss = loss_fn(pred, yb)
				
				# 3. Compute gradients
				loss.backward()
				
				# 4. Update parameters using gradients
				opt.step()
				
				# 5. Reset the gradients to zero
				opt.zero_grad()
			
			# Print the progress
			if (epoch+1) % 10 == 0:
				print('Epoch [{}/{}], Loss: {:.4f}'.format(epoch+1, num_epochs, loss.item()))
	
	model = nn.Linear(2, 3, bias=True)
	loss_fn = F.mse_loss
	opt = nn.optim.SGD(model.parameters(), lr=1e-5)
	ds = TensorDataset(inputs, targets)
	train_ds = ds[0:30]
	train_dl = DataLoader(train_ds, batch_size=8, shuffle=True)
	
	# Train
	fit(100, model, loss_fn, opt, train_dl)
	# Infer
	preds = model(test_inputs)
	```