---
id: infix-postfix-prefix
aliases: []
tags: []
---

## ==Infix Expressions and Their Stack Implementation==

### Infix expressions are written in the form we typically use in pen and paper, such that:

$$
\text{expression} \to \text{operand} \text{  } \text{operator} \text{  } \text{operand}
$$

where:

$$
\text{operand} \to \text{expression} \vee \text{symbol} \vee \text{constant}
$$
$$
\text{operator} \equiv \{*, -, +, /, (, ) \}
$$
$$
\text{symbol} = \{ 'a' \dots 'z',  \dots \}
$$

- **Examples**: ^InfixExamples
	1. \( 1 + 2 - 3 / 5 \)
	2. \( ((9/2) + (3\*8)-5) \)

####	 Evaluation of infix expressions 
	If we ever asked to find the value of an arithmetic expression as show in above examples [[^InfixExamples]] then we first need to create a postfix expression from the infix expression
	then we can evaluate it using stack to get the result.
---

## Prefix Expression

In **prefix notation** (also known as Polish notation), operators appear before their operands. This format is helpful for stack-based evaluation because it eliminates the need for parentheses.

### Grammar
$$
\text{expression} \to \text{operator} \text{ } \text{operand} \text{ } \text{operand}
$$
$$
\text{operand} \to \text{expression} \vee \text{symbol} \vee \text{constant}
$$
$$
\text{operator} \equiv \{ *, -, +, /, (, ) \}
$$
$$
\text{symbol} = \{ 'a' \dots 'z',  \dots \}
$$

- **Examples**: ^e199e1
	1. \( + 1 2 - 3 5 \) 
	2. \( + / 9 2 * 3 8 - 5 \)

---

## Postfix Expression

In **postfix notation** (Reverse Polish Notation or RPN), operators appear after their operands, making it ideal for stack-based evaluation. Like prefix, postfix requires no parentheses for order.

### Grammar
$$
\text{expression} \to \text{operand} \text{ } \text{operand} \text{ } \text{operator}
$$
$$
\text{operand} \to \text{expression} \vee \text{symbol} \vee \text{constant}
$$
$$
\text{operator} \equiv \{ *, -, +, /, (, ) \}
$$
$$
\text{symbol} = \{ 'a' \dots 'z',  \dots \}
$$

- **Examples**:
	1. \( 1 2 + 3 5 / - \) 
	2. \( 9 2 / 3 8 * + 5 - \)

### Conversion of infix expression to postfix expression

- Rules
	1. 

