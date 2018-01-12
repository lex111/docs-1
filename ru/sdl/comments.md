# Комментарии

Комментарии, как и в любом языке служат для документирования исходного 
кода для последущего прочтения их человеком. Такие описательные части 
предназначены только для разработчиков и игнорируются во время компиляции.

```graphql
#
# API приложения
#

type Query {
    user: User!
}

#
# Объекты приложения 
#

type User {
    id: ID!
    login: String!
    # ====================== TODO ======================
    #  Надо потом будет поменять с типа 'String' на тип
    #  'DateTime' для полей 'createdAt' и 'updatedAt'
    # ==================================================
    createdAt: String!
    updatedAt: String 
}
```

Такие комментарииначинаются с символа октото́рпа - `#` (не путать с диезом `♯`) 
и оканчиваются переносом строки `\n` или `0x0A`. Можно безбоязненно описывать в 
комментариях какие-либо внутренние процессы или визуально разделять участки кода.

## Документация исходного кода

Как мы можем уже знать RL/SDL - это серверный декларативный язык 
программирования, который служит в основном для того, чтобы объяснять 
клиенту каким образом общаться с сервером. Т.к. обычные комментарии никак не 
учитываются в ответе, то существует альтернативный вариант описания документации:

```graphql
#
# Объекты приложения 
#
"""
This is the User object in our API. It participates 
in requests A, B and C. And also in the response 
to the authentication request.
"""
type User {
    """
    The primary user ID. Does not participate during the 
    creation of a new User object and is generated independently.
    """
    id: ID!
    
    """
    The system user name. Participates in authentication 
    methods along with the password.
    """
    login: String!
    
    # ====================== TODO ======================
    #  Надо потом будет поменять с типа 'String' на тип
    #  'DateTime' для полей 'createdAt' и 'updatedAt'
    # ==================================================
    """
    Creation date of the User in the format RFC3339.
    """
    createdAt: String!
    
    """
    The date of the User's update in the format RFC3339.
    
    Attention! 
    If the user's data has never been updated after the creation,
    then the update date will be empty (NULL).
    """
    updatedAt: String
}
```

Такие секции называются секциями документации (`Docblocks` или `Docstrings`), 
начинаются и оканчиваются символами `"""` и могут содержать переносы строк и 
вообще любые символы, доступные для [скалярного типа String](/sdl/scalar/string).

Однако, как можно заметить, это не обыкновенные комментарии, а 
полноценная языковая конструкция. А значит у них есть строго ограниченная 
область применения. 

Давайте лучше взглянем на примеры:
```graphql
""" 
Документация любой структуры (и не только) описывается перед первым 
упоминанием ключевого слова: 'type', 'interface', 'union' и т.д.
"""
type Object {
    """
    Документация для полей указывается перед названием этого поля, в нашем случае 'field'. 
    """
    field(
        """ 
        Документация для аргументов аналогична полям и указывается перед именем аргумента ('arg').
        """
        arg: Example
    ): Example
}

"""
Документация для 'Some' (перед ключевым словом 'union')
"""
union Some = String | Object

"""
Документация для '@any' (перед ключевым словом 'directive')
"""
directive @any on FIELD
``` 

!> Если строка комментария внутри секции документации начинается с символа
 октото́рпа, то этот символ не включается в текст комментария: `""" # Пример """` -> `Пример`.