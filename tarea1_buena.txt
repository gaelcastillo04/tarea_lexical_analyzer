%{
#include <stdio.h>
%}
                                                                                           
%%
"//".* printf("COMMENT\n");
"f" printf("floatdcl ");
"i" printf("intdcl ");
"p" printf("print ");
[a-zA-Z]+ printf("id ");
"+" printf("plus ");
"=" printf("assign ");
[0-9]+ printf("inum ");
[0-9]+\.[0-9]+ printf("fnum ");
\n printf("\n");
%%
int yywrap(){
    return 1;
}


int main(int argc, char **argv) {
    FILE    *fd;

    if (argc == 2)
    {
        if (!(fd = fopen(argv[1], "r")))
        {
            perror("Error: ");
            return (-1);
        }
        yyset_in(fd);
        yylex();
        fclose(fd);
    }
    else
        printf("Usage: a.out filename\n");
    return (0);
} 