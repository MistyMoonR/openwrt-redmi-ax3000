include $(TOPDIR)/rules.mk

BOARD:=ipq50xx
BOARDNAME:=Qualcomm Atheros IPQ50XX
SUBTARGETS:=arm aarch64

CPU_TYPE:=cortex-a53
FEATURES:=fpu ramdisk nand squashfs pcie

KERNEL_PATCHVER:=4.4
LINUX_VERSION-4.4:=-qsdk-11.4.0.5

CONFIG_KERNEL_GIT_CLONE_URI:=https://git.codelinaro.org/clo/qsdk/oss/kernel/linux-msm
CONFIG_KERNEL_GIT_REF:=31cfce3e8cccb6ec4a74f9d8aec4a735ac0c40eb

include $(INCLUDE_DIR)/target.mk

define Kernel/Prepare/Default
	$(LINUX_CAT) $(DL_DIR)/$(LINUX_SOURCE) | $(TAR) -C $(KERNEL_BUILD_DIR) $(TAR_OPTIONS)
	$(Kernel/Patch)
	$(if $(QUILT),touch $(LINUX_DIR)/.quilt_used)
endef

KERNELNAME:=Image dtbs

DEFAULT_PACKAGES += \
	uboot-envtools \
	kmod-qca-nss-dp swconfig \
	kmod-qca-nss-drv qca-nss-fw-ipq50xx-retail \
	kmod-ath11k wpad-basic-wolfssl

$(eval $(call BuildTarget))
