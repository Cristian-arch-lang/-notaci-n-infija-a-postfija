def infix_to_postfix(expression):
    """Convierte una expresión infija a notación postfija"""
    precedence = {'+': 1, '-': 1, '*': 2, '/': 2, '^': 3}
    output = []
    stack = Stack()

    tokens = expression.split()


    for token in tokens:
        if token.isalnum():  # Si es operando (número o variable)
            output.append(token)
        elif token in precedence:  # Si es operador
            while (not stack.is_empty() and stack.peek() != '(' and
                   precedence.get(stack.peek(), 0) >= precedence[token]):
                output.append(stack.pop())
            stack.push(token)
        elif token == '(':  # Si es un paréntesis de apertura
            stack.push(token)
        elif token == ')':  # Si es un paréntesis de cierre
            while not stack.is_empty() and stack.peek() != '(':
                output.append(stack.pop())
            stack.pop()  # Eliminar '('

    while not stack.is_empty():  # Vaciar la pila
        output.append(stack.pop())

    return " ".join(output)
