include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

define Device/Default
  PROFILES := Default
  ifeq ($(SUBTARGET),arm)
    KERNEL_LOADADDR := 0x41208000
    DEVICE_DTS_DIR := $(DTS_DIR)
  else
    KERNEL_LOADADDR := 0x41080000
    DEVICE_DTS_DIR := $(DTS_DIR)/qcom
  endif
  DEVICE_DTS = $$(SOC)-$(lastword $(subst _, ,$(1)))
  IMAGES := sysupgrade.tar
  IMAGE/sysupgrade.tar := sysupgrade-tar | append-metadata
endef

define Device/FitImage
  KERNEL_SUFFIX := -fit-uImage.itb
  KERNEL = kernel-bin | gzip | fit gzip $$(DEVICE_DTS_DIR)/$$(DEVICE_DTS).dtb
  KERNEL_NAME := Image
endef

define Device/UbiFit
  KERNEL_IN_UBI := 1
  IMAGES := nand-factory.ubi nand-sysupgrade.bin
  IMAGE/nand-factory.ubi := append-ubi
  IMAGE/nand-sysupgrade.bin := sysupgrade-tar | append-metadata
endef

$(eval $(call BuildImage))
