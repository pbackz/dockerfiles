#The default login for all OVA images is: root:blackarch 
#testing source: docker run -it --rm --tty --privileged blackarchlinux/blackarch
FROM blackarchlinux/blackarch

# WORKAROUND for glibc 2.33
# See https://github.com/actions/virtual-environments/issues/2658
# Thanks to https://github.com/lxqt/lxqt-panel/pull/1562
RUN patched_glibc=glibc-linux4-2.33-4-x86_64.pkg.tar.zst && \
    curl -LO "https://repo.archlinuxcn.org/x86_64/$patched_glibc" && \
    bsdtar -C / -xvf "$patched_glibc"

ENV USER=blackman

RUN useradd blackman && \
    groupadd sudo && \
    usermod -a -G sudo $USER && \
    pacman -Suyy --noconfirm --needed sudo pacman-contrib && \
    paccache -ruk0 && \
    echo "%sudo ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/sudo

USER blackman

RUN sudo pacman -S --noconfirm --needed \
    blackman binutils base-devel vim && \ 
    sudo pacman -S --noconfirm --needed blackarch-wireless && \
    sudo paccache -ruk0

ENTRYPOINT ["bash"]