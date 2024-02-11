1   FUNCTION depth_finder(data, labels, test_data, test_labels, return_dataframe)

2   // Initialize variables  
3    good_depths = empty list  
4    best_depths = empty list 
5    plot_depths = empty list 
6    plot_train_scores = empty list
7    plot_test_scores = empty list 
8    results_table = empty list  

9   // Create figure and axes for plotting  
10   fig, ax1, ax2 = create_figure_with_dual_axes()  

11  // Loop through depth values   
12  FOR depth FROM 2 TO 10:
13      
14      // Train decision tree model on data 
15      tree = train_decision_tree(data, labels, depth=depth)

16      // Make predictions on train and test data
17      train_predictions = predict_with_tree(data)  
18      test_predictions = predict_with_tree(test_data)
       
19      // Calculate R2 performance scores
20      train_score = evaluate(labels, train_predictions)
21      test_score = evaluate(test_labels, test_predictions)  

22      // Print the scores for this depth    
23      print(depth, train_score, test_score) 
       
24      // Store for plotting    
25      add depth to plot_depths
26      add train_score to plot_train_scores
27      add test_score to plot_test_scores
       
28      // Optionally store in table  
29      IF return_dataframe == True:
30          add {depth, train_score, test_score} to results_table  

31      // Check performance for depth list
32      IF train_score > 0.8 AND test_score > 0.8:
33          add depth to best_depths  
34      ELIF train_score > 0.6 AND test_score > 0.6:  
35          add depth to good_depths
           
36  // Create plots   
37  plot(plot_depths, plot_train_scores) on ax1   
38  plot(plot_depths, plot_test_scores) on ax2  

39  // Return depths lists or table
40  IF return_dataframe == True: 
41      convert results_table to dataframe
42      return dataframe  
43  ELSE:   
44      return good_depths, best_depths
