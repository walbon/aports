FROM ghcr.io/walbon/alpine:v3.12

ARG USER=devel
RUN adduser -D $USER
RUN addgroup $USER abuild

RUN echo "Set disable_coredump false" >> /etc/sudo.conf
RUN echo "$USER ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN apk update
RUN apk upgrade
RUN apk add alpine-sdk sudo

ARG USER=devel
RUN echo -e "#include <stdio.h>\n#include <stdint.h>\nint main()\n{\n  long double a = 2.0;\n  __int128 b = 8;\n  printf(\"sizeof(long double) = %ld\", sizeof(long double));\n  printf(\"a * b = %Lf\", a * (long double) b);\n  return 0;\n}\n" > /home/$USER/test-ldouble64.c
RUN chown $USER:$USER /home/$USER/test-ldouble64.c
RUN echo -e "all: \n\tgcc -O0 -mlong-double-64 test-ldouble64.c && ./a.out" > /home/$USER/Makefile
RUN chown $USER:$USER /home/$USER/Makefile
