# AmbiK: Dataset of Ambiguous Tasks in Kitchen Environment

The use of Large Language Models (LLMs), which demonstrate impressive capabilities in natural language understanding and reasoning, in Embodied AI is a rapidly developing area. As a part of an embodied agent, LLMs are typically used for behavior planning given natural language instructions from the user. However, dealing with ambiguous instructions in real-world environments remains a challenge for LLMs. Various methods for task disambiguation have been proposed. However, it is difficult to compare them because they work with different data. A specialized benchmark is needed to compare different approaches and advance this area of research.

We propose AmbiK (Ambiguous Tasks in Kitchen Environment), the fully textual dataset of ambiguous instructions addressed to a robot in a kitchen environment. AmbiK was collected with the assistance of LLMs and is human-validated. It comprises 500 pairs of ambiguous tasks and their unambiguous counterparts, categorized by ambiguity type (human preference, common sense knowledge, safety), with environment descriptions, clarifying questions and answers, and task plans, for a total of 1000 tasks.

# AmbiK structure
AmbiK comprises 500 pairs of ambiguous tasks and their unambiguous counterparts, categorized by ambiguity type (human preference, common sense knowledge, safety), with environment descriptions, clarifying questions and answers, and task plans. The full structure of the dataset with examples is presented in the table below.

 AmbiK lable                        | Description                                                                                    | Example                                                                                                                                                                                                                                                                                                         
------------------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
**Environment short**         | environment in a natural language description                                                           | plastic food storage container, glass food storage container, shepherd's pie, pumpkin pie, apple pie, cream pie, key lime pie, muesli, cornflakes, honey                                                                                                                                                         
**Environment full**          | environment in the form of a list of objects                                                            | a plastic food storage container, a glass food storage container, shepherd's pie, pumpkin pie, apple pie, cream pie, key lime pie, muesli, cornflakes, honey                                                                                                                                                     
**Unambiguous direct**        | unambiguous task with exact names of objects                                                            | Fill the glass food storage container with honey for convenient storage.                                                                                                                                                                                                                    
**Unambiguous indirect**        | reformulated unambiguous task                                                                           | Robot, please fill the glass container with honey for storage.   
**Ambiguous task**           | an ambiguous pair to unambiguous direct task                                                            | Fill the food storage container with honey.                                                                                                                                                                                                                                                 
**Ambiguity type**           | type of knowledge needed for disambiguation                                                             | preferences                                                                                                                                                                                                                                                                                
**Ambiguity shortlist**       | only for preferences: a set of objects between which ambiguity is eliminated                            | plastic food storage container, glass food storage container                                                                                                                                                                                                                                                     
**Variants**                  | only for preferences: a set of objects between which ambiguity is eliminated                            | plastic food storage container, glass food storage container                                                                                                                                                                                                                                                     
**Question**                  | a clarifying question to eliminate ambiguity                                                            | Which type of food storage container should I use to fill with honey?                                                                                                                                                                                                                                            
**Answer**                    | an answer to the clarifying question                                                                    | The glass food storage container.                                                                                                                                                                                                                                                                                
**Plan for unambiguous task** | a detailed plan for the unambiguous task                                                                | 1. Locate the glass food storage container.     2. Locate the honey.    3. Carefully open the honey jar or bottle.   4. Pour honey into the glass food storage container until it is full.   5. Close the honey jar or bottle. 
**Plan for ambiguous task**   | a detailed plan for the ambiguous task                                                                  | 1. Locate the food storage container.   2. Locate the honey.  3. Carefully open the honey jar or bottle.  4. Pour honey into the food storage container until it is full.  5. Close the honey jar or bottle.             
**Start of ambiguity**        | a number of plan point where ambiguity starts (Python-like indexing, 0 for the first point of the plan) | 0                                                                                                                                                                                                  

Every ambiguous task has its unambiguous counterpart, for instance, the task: *Kitchen Robot, please make a hot chocolate by using the coffee machine to heat up milk. Then pour it into **a mug**.* has an unambiguous pair:

*Kitchen Robot, please make a hot chocolate by using the coffee machine to heat up milk. Then pour it into **a ceramic mug**.* 

Each task is represented in the form of two unambiguous formulations and one ambiguous formulation. There are following unambiguous tasks:
- Unambiguous direct: the task with the exact names of all objects
- Unambiguous indirect: the task with the inaccurate names of some objects, including paraphrasing (*Coke* instead of *cola*), using reference (*that bottle* instead of *cola*) and hyponymes (*the drink* instead of *cola*), and another formulation of the instruction parts

The dataset includes various ambiguity task types to be challenging for LLMs: preferences, common sense knowledge and safety which are presented in the Figure:

![Ambiguity types in AmbiK]
([https://github.com/cog-model/AmbiK-dataset/blob/53b8ee3e8312b8a72a1734782b9b7f157314bce7/ambschema.png;base64,iVBORw0KGgoAAAANSUhEUgAAAHoAAABkCAYAAABJhSQPAAAACXBIWXMAAAsTAAALEwEAmpwYAAADf0lEQVR42u3dW2vTYBzH8eeUPDm0adN2adeddNMpo2ObXoypsDvFd+WbEfRSUUHvxIFOEXG7UEFR5xybulO3tU3XpF4JIiJ43Pw/v+8LKP3nQ54nIaTlC2fOXGKIfAKHANAI0AjQCNAI0AjQCNAI0AjQgEaARoBGgEaARoBGgEaARoBGgAY0AjQCNAI0AjQCNAI0AjQCNKARoBGgEaARoNE/T+EQHL4SwXhsCbnrKWvHU3bdV3rHV3rPlXrPkbqppY5tYXUkVx3JZSo4Z4wxkXa7KukmKul2dDvdd+Mk9ltJ7DeTGNAHXFML+Slnu6slnVkpOfm1og5bttC/8lmp4LwtuGhbzGo40t1kFs7ogyjljNV9ZS9V3OB11Su97XUrWLqJFFtcLEdu9vmRTPSq3+vDHk2oli3k66qXWzie7V8r6AIuxogty+/KbvbxydzActmJcNVNrIYW6uloED0ay4/i9opg64GlH4yHgwe57wL6L/YhtN17k4Xh95HT8z99b0D/xBl891Rx5DDuv4D+AzW1kHMThaFnRzOD//McgP5BT0aD6N5UYYzCLID+Th/ztnPzXFSr+ypDZSZAf3MvPF/LVw/7rRKgf6NtX9nXZsvjW1krS3E+QDPGXgz64e2ZngnKMxoPfXeqMPh0NBimPqex0G3FxfXZythKSZdMmNdI6B1XWlcu9J1uauGYMrNx0OuBpS9f7JsxbW6joD+EtnvlfHXaxFVMABnQpJZrk5GNgN51pDJxTzYKuiM5v3q+epoh2tA3zkUn91zpgpkw9P3xfHWp4pZBTBj6bcXNUnwCBeivatlCXpstY1+mDn1nuucYWIlDv+z3cm+qbi9YCUO3FRe3zkZTICUOPV8L+8BJHLruKevJiWAEnMSh5ybDI6AkDr2VUfbLAR/LNnXo+Vo4AEbi0E0t5IshH9DUoRdHggiEBkA/rOWPg5A49GpBeynHD+KRh148lsUjSOrQKWfs2dHMEPiIQ28ElgM6A6Df9Ho50BkA/arfw20VdeiUM7ZW1EXQEYduaIl3uk2A3sjhQswI6PWc7YHNAOjNwAK0CdBbGUAbAb3r4RUbI6BbWtpgMwC6rbgFNgOgv/z1DyIOLdJuF2wGQNud7j7YDIB24qQNNgOgM42kCTYDoPO7+w2wGQAd1gFtBHRxuw1oE6AL2/stsBkA7cVJB2w/32c7r8DNq/e3jAAAAABJRU5ErkJggg==](https://github.com/cog-model/AmbiK-dataset/blob/fec2a1f28e065b45b1eeab4055df1b7ea8896d87/ambschema.png?raw=true))
