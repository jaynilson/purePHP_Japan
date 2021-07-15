# rn Neural Network in pure PHP - ML Machine Learning - AI Artificial Intelligence
RED NEURONAL

 # WHAT IS?:
It is a library for machine learning (deep learning). You can create a neural network structure of the layers we want with the number of neurons we want. Each layer can have a different trigger function. The result can be exported in JSON format to take the trained network to any other server. 100% written in PHP (pure PHP). Easy to use on any type of server.

Easely use. You only need to include a master file .php and with very little code begin to train your data :smiley:

 # SCREENSHOT:
![Screenshot of the neural network written in Pure PHP](https://github.com/vivesweb/rn-Neural-Network-in-pure-PHP-ML-AI/blob/main/Captura-de-pantalla-2021-07-15-a-les-14.00.49.jpg)

 
 # REQUERIMENTS:
 
 - A minimum (minimum, minimum, minimum requeriments is needed). Tested on:
 		
    - Simple Raspberry pi (B +	512MB	700 MHz ARM11) with Raspbian Lite PHP7.3 (i love this gadgets)  :heart_eyes:
 		
    - VirtualBox Ubuntu Server 20.04.2 LTS (Focal Fossa) with PHP7.4.3 
 - Needed 1 hidden layer at least
 
 
  # FILES:
 There are 3 basic files:
 
 rn.class.php -> Neural network class. This file is the main file. This file includes inside rn_layer.class.php
 
 rn_layer.class.php -> Layer class. This file includes inside rn_node.class.php
 
 rn_node.class.php -> Node/Neuron class
 
 
 # INSTALLATION:
 A lot of easy :smiley:. It is written in PURE PHP. Only need to inclue the files. Tested on basic PHP installation
 
 `    require_once( 'rn.class.php' );`
 
 # BASIC USAGE:
 
 - Define train input items array
 
 `    $arrTrainInputItems	= [
    	[0, 0],
	[0, 1],
	[1, 0],
	[1, 1]
     ];`
 
 
 - Define desired output values array
 
`    $arrTrainOutputItems 	= [
	[0.1, 0.2],
	[0.3, 0.4],
	[0.5, 0.6],
	[0.7, 0.8]
     ];`
 
 
 - Create neural network object
 
 `    $rn = new rn( [3, 1, 2] );  // 3x1x2 = 3 layers. 3 input neurons, hidden layer with 1 neuron, 2 output neurons`
 
 If you want for example 4 layers (3x12x8x2): 3 input neurons, hidden layer with 12 neurons, hidden layer with 8 neurons, output layer with 2 neurons, simply do:
 
 `    $rn = new rn( [3, 12, 8, 2] );`
 
 
 - Print All Train Input data, Neural Network Output data & Train Desired Data
 
         $num_sample_data = count($arrTrainInputItems);
    
         echo "Default Values: ".PHP_EOL;
 
         for($i=0;$i<$num_sample_data;$i++){
     
               $rn->EchoOutputValues( $arrTrainInputItems[$i], $arrTrainOutputItems[$i] );
     
         }
     
 
 
 - Do learn process:
 
 `    $rn->Learn($arrTrainInputItems, $arrTrainOutputItems);`
 
 
# RESUME OF METHODS:

- **CREATE NEURAL NETWORK:**
 
$rn = new rn( [ARRAY OF INT] );

Example:

`    $rn = new rn( [3, 1, 2] );  // 3x1x2 = 3 layers. 3 input neurons, hidden layer with 1 neuron, 2 output neurons`



- **PRINT ALL TRAIN INPUT DATA, NEURAL NETWORK OUTPUT DATA & TRAIN DESIRED DATA:**

$rn->EchoOutputValues( $arrTrainInputItems, $arrTrainOutputItems );

Example:

`    $rn->EchoOutputValues( $arrTrainInputItems[$i], $arrTrainOutputItems[$i] );`



- **PROCESS OF LEARN:**

$rn->Learn([ARRAY OF FLOAT], [ARRAY OF FLOAT]);

Example:

`    $rn->Learn($arrTrainInputItems, $arrTrainOutputItems);`



- **SET THE NUMBER OF EPOCHS:**

$rn->fSet_num_epochs( INT ); // Set rn Num Epochs. Default: 1000

Example:

`    $rn->fSet_num_epochs( $NumEpochs );`



- **SET THE ACTIVATION FUNCTION FOR ALL OF LAYERS:**

$rn->fSet_activation_function( STRING ); // ['sigm' | 'tanh'] Default: 'sigm'

Example:

`    $rn->fSet_activation_function( 'sigm' ); // ['sigm' | 'tanh'] Default: 'sigm'`



- **SET THE ACTIVATION FUNCTION FOR ONE LAYER:**

$layer->fSet_activation_function( STRING ); // ['sigm' | 'tanh'] Default: 'sigm'

Example:

`    $rn->layer[1]->fSet_activation_function( 'sigm' ); // ['sigm' | 'tanh'] Default: 'sigm'`


- **SET LEARNING RATE:**

$rn->set_alpha( FLOAT );

Example:

`    $rn->set_alpha( .5 );`



- **GET THE OUPUT VALUE OF NEURAL NETWORK OF ONE OUTPUT NODE:**

- Output node: If we have 2 neurons, we can get the output value for Neuron[0] | Neuron[1]

$rn->run( INT OUTPUT NODE ID, ARRAY OF FLOAT INPUT VALUES );

Example:

`    $rn->run( $id_output_node, $arrInputValues );`


- **GET THE MEANSQUARE ERROR OF THE MODEL:**

$rn->MeanSquareError(ARRAY OF INPUT VALUES, ARRAY OF DESIRED VALUES);

Example:

`    $rn->MeanSquareError($arrTrainInputItems, $arrTrainOutputItems);`


- **EXPORT THE TRAINED MODEL CONFIGURATION TO A STANDARD JSON STRING:**

`    echo $rn->exportData2Json();`


- **IMPORT A TRAINED DATA STRING IN JSON FORMAT TO OUR NEURAL NETWORK CLASS:**

$rn->importJson2Data( STRING JSON );

Example:

    $JsonDataStr = '{"InaticaNeuralNetwork":{"NumInputNeurons":3,"NumOutputNeurons":2,"CreationDate":"2021-07-11 16:59:26","NumTotalLayers":3,"NumHiddenLayers":1,"NumEpochs":1000,"MeanSquareError":0.0006291862647577675,"Layers":[{"Layer":{"num_nodes":3,"imFirst":true,"imLast":false,"activation_function":"sigm","bias":-2.2457597339700284,"Nodes":[{"Node":{"arr_weights_to_next_layer":[0.5]}},{"Node":{"arr_weights_to_next_layer":[2.9314473212095957]}},{"Node":{"arr_weights_to_next_layer":[1.9449224564817373]}}]}},{"Layer":{"num_nodes":1,"imFirst":false,"imLast":false,"activation_function":"sigm","bias":-2.0579661087844885,"Nodes":[{"Node":{"arr_weights_to_next_layer":[3.0701300830533205,3.739411894753024]}}]}},{"Layer":{"num_nodes":2,"imFirst":false,"imLast":true,"activation_function":"sigm","bias":0.5,"Nodes":[{"Node":{"arr_weights_to_next_layer":0.5}},{"Node":{"arr_weights_to_next_layer":0.5}}]}}]}}';
      
    $JsonData = json_decode( $JsonDataStr );
      
    $rn->importJson2Data($JsonData->InaticaNeuralNetwork);
 
 - **INFORM ABOUT THE LEARNING PROCESS**

We can to do echoes of the actual neural network process with 2 variables of the network class:
$rn->InformEachXBlock
$rn->InformEachXEpoch

If the process of learning is really fast, we can use InformEachXEpoch, for example, for do one echo of the values every 100 Epochs:

`    $rn->InformEachXEpoch = 100;`

If the process of learning is tooooo slooooow, we can use InformEachXBlock, for example, for do one echo every block of 10 samples learned:

`    $rn->InformEachXBlock = 10;`
 
 
 
 # FUTURE PLANS
 
 Machine learning is magic. Artificial intelligence is an exciting world, but deep learning process at Backpropagation algorithm take a lot of time. PHP is not the most efficient programming language for do tasks of deep learning, but it is perhaps the most extensive programming language in the world (and i love it ^_^). The opportunity to train complex models on local machines without need to install almost anything and implement them on STANDARD production servers (like shared hosting services) without need to configure anything, gives a clear advantage to this programming model.
 
 
 **1) SOME BUG. NOT 100% GOOD RESULTS IN MEANSQUARE ERROR:**
 
 The system of obtaining the quadratic error of the network will surely be changed, since the current system looks for the error on the first 100 data of the model to be learned (so as not to perform the calculation on the entire entire database). An alternative solution will be sought to improve the accuracy of the error.
 
 
 
 **2) ADD SOME FEATURES**
 
 I have in mind to implement different characteristics to the class, such as momentum, other activation functions as RELU or SOFTMAX, .... among others.
 
 It would be very interesting to add specific functions to speed up programming and its use in convolutional neural networks.
 
 Another interesting feature will be to add to the class the option to save or read the current configuration of the neural network learned data from a file. Currently, it is possible to import and export the configuration of our network using the JSON data format as input or output, but reading and writing these same data into files would speed up many processes in an automated way.
 
 As an extra utility, we also want to prepare the system so that it can obtain the train, desired and evaluation data directly from .CSV files.



 ### ACCELERATE LEARNING SPEED
 
 
 **3) MULTITHREAD & MULTI-PROCESSORS**
 
 One solution to improve the speed spend in the process of deep learning is using multi-processor threads (process parallelization)... and YES. PHP can do it!!!!
 
 With php, parallelization is possible, then i will have new code soon for the class with parallelization feature. This code will need to be executed on linux servers and CLI environtment, but the code for execute learned models will be remain standar for execute it on any type of standard server as a basic web server with PHP installation, for example (CLI, cgi, windows, linux, web server on shared hosting, ....).
 
 You need to wait some time.... Why? My life is not only virtual and PHP ;D, but i promise to upload the code as fast as i can. There are many problems that can arise when working with multithreads (system messages between processes, shared memory between them, ...). All this must be controlled correctly by means of semaphores so that some processes do not interfere with others giving system errors ... and as if that were not enough, the temperature of the CPU must be controlled, since the deep learning process is a hard task for the processor. Have you put your processor at 100ºC doing deep learning? I do.... in case you are curious to know what happens, the server stops immediately  :sweat_smile: :man_facepalming:
 
  ### THE GREAT PROJECT
  
 **4) DEEP LEARNING SERVER FARM WITH PHP**

 The last step will be to create a service of Deep Learning Server Farm... but we need to wait. Everything will come in due time. Much work remains to be done before :smiley:
 
 
 
 
 @author Rafael Martin Soto
 
 @author {@link http://www.inatica.com/ Inatica}
 
 @since July 2021
 
 @version 1.0
 
 @license GNU General Public License v3.0
 
 
 A LOT OF THANKS TO:
 
 *   https://github.com/infostreams/neural-network/blob/master/class_neuralnetwork.php
 *   https://gist.github.com/ikarius6/26851fb7220837e8016fe0c425d34dd6
 *   https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/
 *   https://www.youtube.com/channel/UCy5znSnfMsDwaLlROnZ7Qbg
