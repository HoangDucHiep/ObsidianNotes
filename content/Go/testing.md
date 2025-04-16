---
title: testing
tags:
  - Go
---
- Tất cả các test có 4 bước chính:
	- The preparation phase: set up tất cả các thứ cần cho việc test - input values, expected output, environment variables, global variables, network connections, etc.;
	- The execution phase, khi ta gọi tested function - thường chỉ là 1 dòng duy nhất
	- The decision phase, where we check the output we got corresponds to the output we want - this might include several comparisons, evaluations, and sometimes some processing - and have the test either fail or pass; 
	- The teardown phase, where we kindly clean back to whatever the state was prior to the test’s execution - this step is made extremely simple thanks to Go’s defer keyword: anything that was altered or created during preparation should be fixed or destroyed here.