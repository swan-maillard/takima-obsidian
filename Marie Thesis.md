## Feedback

### Introduction

- The introduction feels too advanced for readers unfamiliar with the topic. For example:
    
    > _“Kernel-based methods have attracted significant attention, particularly those formulated in the context of Reproducing Kernel Hilbert Spaces (RKHS).”_

    This kind of sentence is hard to parse without prior knowledge. Consider introducing the concepts more gradually, perhaps by briefly explaining what kernel-based methods are and why they're useful in practice, before diving into RKHS.

### Section 2.1.8 – Summary

- This summary is helpful — it gives a better sense of the mathematical content even for readers like me who didn’t dive deep into all the equations.

- That said, it could be made even clearer. Try framing it as if you were explaining it to someone unfamiliar with functional analysis.

- For example:
> _“This provides the framework for defining Cauchy sequences, which are essential for defining completeness of a space.”_  
        
   This felt abstract — it would help to clarify _why_ completeness matters and _how_ Cauchy sequences relate to it in simple terms.

- Similarly:
> _“Banach spaces are complete normed vector spaces, and equipping this with inner products creates Hilbert spaces.”_  
    
Raised questions for me:
- What is a complete normed vector space, and what does that actually _enable_?   
- Why does adding inner products matter?
- Most importantly: how is any of this connected to your core research questions?     

### Section 2.2 – RKHS Definition

> _“A Reproducing Kernel Hilbert Space (RKHS) is a Hilbert space of functions with unique properties that enable complex function spaces to be analysed and manipulated through kernel function.”_

- This sentence is conceptually dense. You could break it down or rephrase to clarify _what_ these unique properties are, and _how_ they are useful in practical terms.

### Section 2.2.2 – Self-Adjointness

> _“The Gram operator K is self-adjoint.”_
- A short explanation of what _self-adjoint_ means  would be helpful

### Section 2.5.5 – Cones

- I didn’t understand the purpose of introducing _cones_. It would help to explain:
    - Why this concept is relevant at this point in the text.
    - What role it plays in the overall argument or application.

### General Feedback

- **Abstract and introduction are too technical and math-heavy.** It was hard for me to grasp the bigger picture or motivation for your work at the start. I found myself disengaged before reaching the parts that I could relate to (chapters 4–7).

- Chapters 4–7 are much more accessible and clearly rooted in practical concerns — they made your research goals and methods much clearer. It might be worth reflecting that balance earlier in the document, especially in the abstract and introduction.

- **Suggestion**: For each major mathematical section, consider adding a short “preview” paragraph before the math-heavy content. It could explain:
    - What the upcoming concepts aim to achieve
    - Why they matter in the context of your work

- Similarly, the **section summaries** are helpful, but could be even more effective if they included:
    - A plain-language interpretation of the results or theory
    - A brief statement about how it connects back to real-world applications or later chapters


## Typos

- Page 16, 1.1 : **"Chapter ??**"
- Page 18, 1.4: 
	- "Chapter 2 cover" => **covers**
	- "and introduce" => **introduces**
	- "Chapter 5 outline" => **outlines**
- 2.2.4: "**hypothesis** space of functions", "induced **hypothesis** class " => Typo?
- Page 28, 2.2.8: 
	- "RKHS provide" => **provides**
	- "Central to this framework is the feature map" => Weird way of phrasing
	- "which allow" => **allows**
	- "implicitly define" => **defines**
	- " Together, RKHS theory enable" => "Together" but then you only talk about RKHS. Together with what?
- Page 31, *Function Space L2(D)*: 
	- "**the** both the Legendre and Chebyshev"
	- "**is,** respectively, are then given by"
- Page 40, 2.5.6: "convex optimisation provide" => **provides**
- Page 44, 4: "benchmark dynamic systems" => **benchmarked?** / **benchmark of the?**
- Page 59, equation (4.35): "of the spring, respectively" => **"."** is missing
- Page 83, 6.2.3: "The following section show" => **shows**
- Page 87, 6.3: 
	- "Figure 6.3.1 show" => **shows**
	- "Figure 6.3.2 show" => **shows**
