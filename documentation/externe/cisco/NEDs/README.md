









 
 
   <link rel="stylesheet" href="/etc/designs/cdc/transformation/wemdcmt_responsive.css"> 
   <link rel="stylesheet" href="/etc/designs/cdc/transformation/wemdcmt_responsive.css"></code> 
  <div class="WordSection1"> 
   <p class="pIntroCMT">Exceptional Multivendor Support through Network Elements Drivers</p> 
   <p class="pBody">Cisco<span class="Superscript"><sup class=" cSuperscript">®</sup></span> Network Services Orchestrator (NSO) provides a single pane of glass for orchestrating a multivendor network. To offer support for an exceptional range of multivendor devices, it uses Network Element Drivers (NEDs). Traditionally, device adaptors are a major roadblock, since they cannot be upgraded at the same pace as device interfaces, and adding support for new devices can take months. Cisco NSO NEDs, in contrast, are either generated automatically from the device YANG model, or can add new commands and devices in a matter of weeks. Using NEDs, NSO makes device configuration commands available over a network wide, multivendor Command Line Interface (CLI), APIs, and user interface. In addition, NSO services, like VPN, can configure a complex multivendor network.</p> 
   <p class="pSubhead1CMT">NED overview</p> 
   <p class="pBody">Network element drivers comprise the network-facing part of NSO. They communicate over the native protocol supported by the device, such as Network Configuration Protocol (NETCONF), Representational State Transfer (REST), Extensible Markup Language (XML), CLI, and Simple Network Management Protocol (SNMP).</p> 
   <div class=" pDefault"> 
    <b><span style="font-family:&quot;CiscoSans Light&quot;,&quot;sans-serif&quot;">Figure 1.&nbsp; <span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp; </span></span></b>NEDs in Cisco NSO 
   </div> 
   <p class="pBody"><a href="https://www.cisco.com/c/dam/en/us/products/collateral/cloud-systems-management/network-services-orchestrator/datasheet-c78-734669.doc/_jcr_content/renditions/datasheet-c78-734669_0.jpg" class="show-image-alone" title="Related image, diagram or screenshot."><img id="Picture 0" src="/c/dam/en/us/products/collateral/cloud-systems-management/network-services-orchestrator/datasheet-c78-734669.doc/_jcr_content/renditions/datasheet-c78-734669_0.jpg" alt="datasheet-c78-734669_0.jpg" height="355" width="624"></a></p> 
 
 ![On va voir](https://github.com/Jean-Baptiste-Lasselle/cisco-nso-first-dive/blob/master/documentation/externe/cisco/NEDs/CISCO_NSO_NEDs_datasheet-c78-734669_0.jpg)
 
   <p class="pBody" style="page-break-before:always">Drivers are rendered based on a Yet Another Next Generation (YANG) data model, which provides several benefits:</p> 
   <p class="pBulletCMT" style="font-style: normal; font-variant: normal; font-weight: normal;margin-bottom: 3pt; margin-right: 0pt; margin-top: 0pt; text-decoration: none; text-transform: none"><span style="font-size:7.0pt;font-family:&quot;Arial&quot;,&quot;sans-serif&quot;;position:relative;top:-.5pt">●<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp; </span></span>Drastically shortened development and update cycles: In other systems, adaptors are normally handcrafted. In NSO, however, the NEDs are rendered from a YANG data model that can automatically generate the corresponding commands, such as CLI commands. Typically adding new commands to an existing NED takes a couple of weeks, and creating a new NED takes six to eight weeks. This may however vary with the size and complexity of the configuration.</p> 
   <p class="pBulletCMT" style="font-style: normal; font-variant: normal; font-weight: normal;margin-bottom: 3pt; margin-right: 0pt; margin-top: 0pt; text-decoration: none; text-transform: none"><span style="font-size:7.0pt;font-family:&quot;Arial&quot;,&quot;sans-serif&quot;;position:relative;top:-.5pt">●<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp; </span></span>If the device offers a NETCONF/YANG interface then no development is required, as the NED can be generated automatically from the device model. In this case there is no charge for the NED, so integration is free!</p> 
   <p class="pBulletCMT" style="font-style: normal; font-variant: normal; font-weight: normal;margin-bottom: 3pt; margin-right: 0pt; margin-top: 0pt; text-decoration: none; text-transform: none"><span style="font-size:7.0pt;font-family:&quot;Arial&quot;,&quot;sans-serif&quot;;position:relative;top:-.5pt">●<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp; </span></span>Uniform data model across the network: Across the NSO interfaces and APIs, it appears as though all devices support YANG, although the underlying mechanism can be CLI or REST, for example.</p> 
   <p class="pBulletCMT" style="font-style: normal; font-variant: normal; font-weight: normal;margin-bottom: 3pt; margin-right: 0pt; margin-top: 0pt; text-decoration: none; text-transform: none"><span style="font-size:7.0pt;font-family:&quot;Arial&quot;,&quot;sans-serif&quot;;position:relative;top:-.5pt">●<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp; </span></span>NSO NEDs also provide transactionality for nontransactional devices. The NSO transactional engine can drive the NEDs to do atomic changes and rollback on failure, even when a device has no native support for transactions. Transactional behaviour significantly reduces the volume of code, cost of development and maintenance, and time to market for your service applications.</p> 
   <p class="pTableCaptionCMT"><b><span style="font-family:&quot;CiscoSans Light&quot;,&quot;sans-serif&quot;">Table 1.<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></b>Snapshot of available NEDs</p> 
   <div style="overflow-x: auto;"> 
    <table cellspacing="0" cellpadding="6" bordercolor="#ADADAD" border="1" width="100%"> 
     <tbody> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco Aireos</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Affirmed Acuitas</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Huawei VRP</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco APIC DC (ACI)</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">ALU OmniSwitch</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">IDirect Pulse</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco ASA</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">ALU SAM</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Infoblox</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco DCNM</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">ALU SR</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Juniper JunOS</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco ESA</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Amazon AWS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">MRV Optiswitch</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco GSS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Arista EOS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">OneAccess OneOS</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco IOS &amp; IOS XE</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Avi Vantage</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Openstack</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco IOS XR</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Aviat</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Overture 1400</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco ME1200</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Brocade Ironware</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Overture 5K</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco ME4600</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Brocade NOS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Overture 6K</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco Meraki</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Ceragon IP10</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Palo Alto Networks Panos</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco NXOS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Checkpoint</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Procera PLOS</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco PNR</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Ciena ESM</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Quagga BGP AOS</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">Cisco QPS</p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Ciena SAOS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Redback SE</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco SMA</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Citrix Netscaler</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Riverbed Steelhead</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco STAROS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Clavister COS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Secure64 SourceT</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco UCS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Coriant SDNTC</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Sumitomo EPON</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco WAAS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Datacom DM</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Telco Systems Binox</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Cisco WSA</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">F5 BigIP</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Unix Bind</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">A10 ACOS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">F5 BigIQ</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">VmWare Vcenter</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Accedian NID</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Fortinet FW</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Vyatta VC</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">ADTRAN AOS</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">HPE VCM</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">ZenOSS</span></p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Adva-825</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">Huawei iManager</span></p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none"><span style="border:none windowtext 1.0pt;padding:0in">ZTE XPON</span></p> </td> 
      </tr> 
     </tbody> 
    </table> 
   </div> 
   <p class="pBody" style="margin-top:7.0pt">Note that the NEDs listed in Table 1 is a subset of those available as of July 2017. New NED types are added every month resulting from customer requests.</p> 
   <p class="pTableCaptionCMT" style="page-break-before:always"><b><span style="font-family:&quot;CiscoSans Light&quot;,&quot;sans-serif&quot;">Table 2.<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></b>Features and benefits</p> 
   <div style="overflow-x: auto;"> 
    <table cellspacing="0" cellpadding="6" bordercolor="#ADADAD" border="1" width="100%"> 
     <tbody> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_headCMT" style="font-style: normal; font-variant: normal; font-weight: bold; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-indent: 0pt; text-transform: none">Feature</p> </td> 
       <td> <p class="pChart_headCMT" style="font-style: normal; font-variant: normal; font-weight: bold; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-indent: 0pt; text-transform: none">Benefit</p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">Multivendor library</p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">Orchestrate the Cisco network, as well as all other major vendors.</p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">Rendering from data models</p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">Turn around new or updated NEDs in days or weeks.</p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">YANG data models</p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">Abstract vendor protocols for significantly faster service definitions and OSS integrations.</p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">Transactionality</p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">Reduce error handling.</p> </td> 
      </tr> 
      <tr align="left" valign="top"> 
       <td> <p class="pChart_subheadCMT" style="font-style: normal; font-variant: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">Low cost of device integration</p> </td> 
       <td> <p class="pChart_bodyCMT" style="font-style: normal; font-variant: normal; font-weight: normal; margin-bottom: 3pt; margin-left: 3pt; margin-right: 3pt; margin-top: 3pt; text-align: left; text-decoration: none; text-indent: 0pt; text-transform: none">NETCONF/YANG NEDs are generally free, and NEDs for legacy protocols are sold at a fixed price without recurring development charges.</p> </td> 
      </tr> 
     </tbody> 
    </table> 
   </div> 
   <p class="pSubhead1CMT">Multivendor service agility</p> 
   <p class="pBody">Cisco NSO enabled by Tail-f simplifies the process of provisioning and controlling applications and services in both physical and virtual networks. It decouples network services from specific components, while automatically configuring the network according to the service specifications. </p> 
   <p class="pBody">Few other products on the market can perform network service orchestration with the multivendor capabilities supported by the NEDs. Real networks are always a mix of vendors. To reduce cost and introduce new capabilities, this mix is constantly changing, and devices are upgraded. If an orchestrator cannot address these changes, the network very soon degrades.</p> 
   <p class="pBody">Because the list of NSO NEDs is constantly growing, the Cisco NSO allows true multivendor service agility as changes are implemented, today and in the future.</p> 
   <p class="pSubhead1CMT">Cisco Capital</p> 
   <p class="pSubhead2CMT" style="margin-top:0in">Financing to help you achieve your objectives</p> 
   <p class="pBody">Cisco Capital can help you acquire the technology you need to achieve your objectives and stay competitive. We can help you reduce CapEx. Accelerate your growth. Optimize your investment dollars and ROI. Cisco Capital financing gives you flexibility in acquiring hardware, software, services, and complementary third-party equipment. And there’s just one predictable payment. Cisco Capital is available in more than 100 countries. <a href="https://www.cisco.com/web/ciscocapital/americas/us/index.html">Learn more</a>.</p> 
   <p class="pBody">&nbsp;</p> 
   <p class="pBody">&nbsp;</p> 
   <p class="pBody">&nbsp;</p> 
  </div>
 



