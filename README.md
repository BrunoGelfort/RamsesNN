# RamsesNN
Summary of the main code snipplets used during my master's thesis "Embedding Neural Networks into Dynamic Power System Simulators"

Here is an example workflow to navigate through this repository:
1) First, the neural network should be trained and exported in .onnx (Open Neural Network Exchange) format. In Python, using PyTorch:
   torch.onnx.export(model, init_cond, "NN.onnx"),
   where init_cond is an example input of the neural network.
2) Then, the tutorial roseNNa_tutorial should be followed to transform the .onnx files to those readable by roseNNA.
3) Finally, in the FORTRAN code, the functions from the roseNNa library are added to the solution. Then, the following lines are added to call the Neural Network:
   program NN_program
     use rosenna
     ...
     ! Define and initialise values for the nn inputs and outputs
     real(real64), dimension(1,10) :: nn_input     ! Example input with 10 features
     real(real64), dimension(1,9)  :: nn_output   ! Example output with 9 features

     ! Initialise rosenna
     call initialize_nnx()

     ! NN forward pass
     call use_model(pinn_input, pinn_output)

   Once the code is written, the program NN_program should be added into the workflow of the code. in RAMSES, the power system model should be added to the lists of models.

   4) A further update of this repository will include the whole pipeline from PINN training to RAMSES simulations. 
