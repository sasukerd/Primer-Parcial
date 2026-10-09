# Nombres técnicos — Aplicación **Consignación**

**Origen:** Odoo Studio (carpeta `studio_customization`)
**Módulo exportado:** `studio_customization` (versión `19.0.1.0`)
**Módulo base de la app:** `consignacion_studio`
**Autor / Empresa:** Blu Pharma SRL

## Dependencias del módulo (`__manifest__.py`)

```
ai_documents_account
ai_server_actions
consignacion_studio
mrp
pos_settle_due
web_grid
web_hierarchy
whatsapp
worksheet
```

---

## 1. Modelos

### 1.1 Modelos propios (definidos en este módulo)

| Nombre técnico | Nombre visible |
|---|---|
| `x_liquidacion_de_cobra` | 💸Liquidación de Cobranza |
| `x_comision_por_lote` | 🧾Comisión Por Lote |
| `x_comision_por_lote_line_4fbf2` | comision_por_lote_line |
| `x_comision_por_lote_line_bfd8a` | comision_por_lote_line |

### 1.2 Modelos referenciados de `consignacion_studio`

| Nombre técnico | Descripción |
|---|---|
| `x_perdidas_sc` | Pérdidas |
| `x_gestion_de_devolucio_sc` | Gestión de devolución (RMA) |
| `x_validador_de_pin_sc` | Validador de PIN |
| `x_lertas_de_reabas_sc` | Letras / Solicitudes de reabastecimiento |
| `x_asignar_personal_sc` | Asignar personal (regla de comisión) |
| `x_test_sc` | Test / Registrar Consumo |
| `x_facturas_clientes_sc` | Facturas Clientes |

### 1.3 Modelos estándar de Odoo customizados

| Nombre técnico |
|---|
| `sale.order` |
| `mrp.production` |
| `purchase.order` |
| `product.template` |
| `stock.location` |
| `account.move` |
| `res.partner` |
| `hr.employee` |

---

## 2. Campos técnicos (`ir.model.fields`)

### 2.1 `x_liquidacion_de_cobra` (💸Liquidación de Cobranza)

| Campo técnico | Tipo | Etiqueta |
|---|---|---|
| `x_name` | char | Descripción |
| `x_active` | boolean | Activo |
| `x_studio_sequence` | integer | Secuencia |
| `x_studio_empleado` | many2one (`hr.employee`) | Empleado |
| `x_studio_selection_field_2r6_1k3s2b7q3` | selection | Barra de estado de flujo |
| `x_studio_fecha_inicio` | date | Fecha Inicio |
| `x_studio_fecha_fin` | date | Fecha Fin |
| `x_studio_porcentaje_de_comision` | float | Porcentaje de Comisión |
| `x_studio_total_operaciones` | float | Total Operaciones |
| `x_studio_total_efectivo` | float | TOTAL EFECTIVO |
| `x_studio_total_tarjeta` | float | TOTAL TARJETA |
| `x_studio_total_transacciones` | float | TOTAL TRANSACCIONES |
| `x_studio_float_field_9gg_1k3s6n048_1` | float | (-) DEVOLUCIONES / NC |
| `x_studio_base_neta_sin_itbis` | float | BASE NETA (SIN ITBIS) |
| `x_studio_comision_a_pagar` | float | COMISIÓN A PAGAR |
| `x_studio_facturas_seleccionadas` | many2many (`account.move`) | Facturas Seleccionadas |
| `x_studio_rma_relacionados` | many2many (`x_gestion_de_devolucio_sc`) | RMA Relacionados |
| `x_studio_regla_de_comision` | many2one (`x_asignar_personal_sc`) | Regla de Comisión |
| `x_studio_facturas_a_liquidar` | many2many (`account.move`) | Facturas a Liquidar |
| `x_studio_many2many_field_5hp_1k3ubqkj3` | many2many (`x_perdidas_sc`) | Nuevo Many2Many |

Valores de la barra de estado: `Borrador`, `Calculado`, `Aprobado`, `Pagado` (+ `Cancelado` en vistas).

Tablas de relación: `x_account_move_x_liquidacion_de_cobra_rel`, `x_account_move_x_liquidacion_de_cobra_rel_1`, `x_x_gestion_de_devolucio_sc_x_liquidacion_de_cobra_rel`, `x_x_liquidacion_de_cobra_x_perdidas_sc_rel`.

### 2.2 `x_comision_por_lote` (🧾Comisión Por Lote)

| Campo técnico | Tipo | Etiqueta |
|---|---|---|
| `x_name` | char | Descripción |
| `x_studio_sequence` | integer | Secuencia |
| `x_studio_fecha_de_inicio` | date | Fecha de Inicio |
| `x_studio_fecha_de_fin` | date | Fecha de Fin |
| `x_studio_selection_field_632_1k464f74e` | selection | Barra de estado de flujo |
| `x_studio_one2many_field_9lp_1k464hh8t` | one2many (`x_comision_por_lote_line_4fbf2`) | Nuevas líneas |
| `x_studio_liquidaciones_del_lote` | one2many (`x_comision_por_lote_line_bfd8a`) | Liquidaciones del Lote |

Valores de la barra de estado: `Borrador`, `Procesado`, `Pagado`.

### 2.3 `x_comision_por_lote_line_4fbf2`

| Campo técnico | Tipo | Etiqueta |
|---|---|---|
| `x_name` | char | Descripción |
| `x_studio_sequence` | integer | Secuencia |
| `x_comision_por_lote_id` | many2one (`x_comision_por_lote`) | X Comision Por Lote |

### 2.4 `x_comision_por_lote_line_bfd8a`

| Campo técnico | Tipo | Etiqueta |
|---|---|---|
| `x_name` | char | Descripción |
| `x_studio_sequence` | integer | Secuencia |
| `x_comision_por_lote_id` | many2one (`x_comision_por_lote`) | X Comision Por Lote |
| `x_studio_empleado` | many2one (`hr.employee`) | Empleado |
| `x_studio_currency_id` | many2one (`res.currency`) | Currency |
| `x_studio_total_cobrado` | monetary | Total Cobrado |
| `x_studio_comision` | monetary | Comisión |
| `x_studio_ver_detalle_individual` | many2one (`x_liquidacion_de_cobra`) | Ver Detalle Individual |

### 2.5 Extensión en `sale.order`

| Campo técnico | Tipo | Etiqueta |
|---|---|---|
| `x_studio_metodo_de_pago` | selection | Metodo de Pago (`efectivo`, `tarjeta`, `transferencia`) |

### 2.6 Campos de modelos referenciados (usados en vistas / acciones)

**`x_perdidas_sc`**: `x_studio_state`, `x_studio_registrado_por`, `x_studio_date_1`, `x_studio_producto_sc`, `x_studio_ubicacion`, `x_studio_cantidad_perdida`, `x_studio_motivo_de_la_perdida`, `x_studio_costo_unitario`, `x_studio_precio_venta`, `x_studio_costo_total`, `x_studio_venta_potencial`, `x_studio_ganancia_neta_1`, `x_studio_evidencias`

**`x_gestion_de_devolucio_sc`**: `x_studio_venta_origen`, `x_studio_cliente`, `x_studio_proveedor`, `x_studio_motivo`, `x_studio_monto_a_reembolsar`, `x_studio_currency_id`, `x_studio_nota_de_credito_relacionada`, `x_studio_estado_del_rma`, `x_studio_one2many_1`, `x_studio_producto_sc`, `x_studio_cantidad_sc`, `x_active`

**`x_lertas_de_reabas_sc`**: `x_studio_estado`, `x_studio_empleado`, `x_studio_cliente`, `x_studio_fecha`, `x_studio_many2one_1`, `x_studio_forzar_envio`, `x_studio_one2many_5`, `x_studio_producto_sc`, `x_studio_cantidad_sc`, `x_studio_sequence`

**`x_asignar_personal_sc`**: `x_studio_cliente`, `x_studio_empleado`, `x_studio_ubicacion`, `x_active`, `x_studio_porcentaje_sobre_margen`, `x_studio_lista`, `x_studio_minimo_de_entregas`, `x_studio_producto_sc`, `x_studio_sequence`

**`x_validador_de_pin_sc`**: `x_studio_pin`, `x_studio_perdida_id`

**`x_test_sc`**: `x_studio_estado`, `x_studio_ubicacion`, `x_studio_partner_id`, `x_studio_user_id`, `x_studio_date`, `x_studio_motivo`, `x_test_line_ids_b1d32`, `x_studio_cantidad_sc`, `x_studio_stock`, `x_studio_costo_unitario`

**`stock.location`**: `x_studio_total_existencias_sc`

**`sale.order`**: `x_studio_porcentaje_de_flete_sc`

---

## 3. Acciones de ventana (`ir.actions.act_window`)

| ID / Nombre técnico | Nombre | Modelo |
|---|---|---|
| `ubicaciones_34ad2868-af19-440c-ad48-5bf97f6b7cf7` | 📍 Ubicaciones | `stock.location` |
| `facturas_clientes_144a8edc-eae4-4663-a55e-7a023fd875c3` | 📤 Facturas Clientes | `x_facturas_clientes_sc` |
| `facturas_clientes_28fb6ea0-dd0b-4826-a9e1-c6f29e012cc3` | 📤 Facturas Clientes | `account.move` |
| `contactos_58407d0c-430f-45ab-b9c7-6d43aad0028d` | 📇 Contactos | `res.partner` |
| `liquidacion_de_cobra_75351106-334c-4799-bb18-0e29bdc1fdbc` | 💸Liquidación de Cobranza | `x_liquidacion_de_cobra` |
| `asdaas_ba154e72-00ce-4923-b9df-58e0659d8bb3` | asdaas | `x_validador_de_pin_sc` |
| `comision_por_lote_90978f95-da2f-4cce-875b-c2ad76bbe028` | 🧾Comisión Por Lote | `x_comision_por_lote` |

---

## 4. Acciones de servidor (`ir.actions.server`)

| Nombre técnico | Nombre | Modelo | Estado |
|---|---|---|---|
| `consignacion_studio.confirmar_perdida_24a640e7-55c7-4516-b624-77a9167d41fa` | Confirmar pérdida | `x_perdidas_sc` | code |
| `consignacion_studio.registrar_consumo_6610ec81-589e-4720-b2a4-44ab396c8648` | Registrar Consumo | `x_test_sc` | code |
| `consignacion_studio.ejecutar_codigo_c27c1f8c-8c28-4d6b-b645-d0d31c8279fc` | Ejecutar código | `x_gestion_de_devolucio_sc` | code |
| `consignacion_studio.perdida_enviar_a_val_8f483eee-1b23-4043-8ca7-c82baedb571e` | Pérdida: Enviar a Validación | `x_perdidas_sc` | code |
| `consignacion_studio.ejecutar_codigo_a5f5e296-fa1b-4dea-9cf8-76b61a7a976c` | Ejecutar código | `x_validador_de_pin_sc` | code |
| `ejecutar_codigo_2ab6b59e-7f6b-4674-93a5-2e8ee4155e0e` | Calcular Cobros (Sin ITBIS) | `x_liquidacion_de_cobra` | code |
| `ejecutar_codigo_eea999f4-1af8-45c6-b4ff-95f34d3d62d3` | Aprobar Liquidación | `x_liquidacion_de_cobra` | code |
| `ejecutar_codigo_99fd1aaf-032f-432b-8d43-496ea5bdb551` | Volver a Borrador | `x_liquidacion_de_cobra` | code |
| `cancelar_e2c3f52e-d561-49b1-809a-3d66a71f1865` | Cancelar | `x_liquidacion_de_cobra` | object_write |
| `ejecutar_codigo_6c7700db-e0bc-4ecd-a7e4-28f335a31af6` | Ejecutar código | `x_liquidacion_de_cobra` | code |
| `ejecutar_codigo_7740770a-2f39-49a2-a98e-bfd92cac930b` | Ejecutar código | `x_liquidacion_de_cobra` | code |
| `ejecutar_codigo_b9e4a962-0cc7-4c4b-98e9-50c43a54894a` | Ejecutar código | `sale.order` | code |
| `ejecutar_codigo_acef3262-b541-4ee1-8c4b-dcb58c259855` | Ejecutar código | `mrp.production` | code |
| `ejecutar_codigo_6f59a5e0-1103-465b-a50b-65c691874dc4` | Ejecutar código | `sale.order` | code |
| `ejecutar_codigo_c3510fb2-4bc3-4e92-a282-676f45c66058` | Calculo Por lote | `x_comision_por_lote` | code |
| `ejecutar_codigo_617b4a9b-2a97-4b33-846f-68feda2d8458` | Ejecutar código | `mrp.production` | code |

> Nota: la acción `consignacion_studio.validacion_c24db260-ca10-46cb-891d-1fa3601464f8` ("Validar Pérdida") se referencia desde la vista pero no está exportada.

---

## 5. Menús (`ir.ui.menu`)

| Nombre técnico | Nombre | Menú padre (ref) |
|---|---|---|
| `consignacion_ubicaci_f2b00661-56a0-4b29-964b-4e66e9458653` | 📍 Ubicaciones | `consignacion_studio.asdasd_22e514c6-6109-4699-bf21-dfd662a34468` |
| `consignacion_factura_951166a9-ffbe-47ef-bb70-5e608d4f25e1` | 📤 Facturas Clientes | `consignacion_studio.asdasd_facturas_bc9a5af3-978f-431d-a8d9-35e2cd925a0a` |
| `consignacion_contact_26bad2af-3202-422d-b8e6-cca2c92f3f6e` | 📇 Contactos | `consignacion_studio.asdasd_contactos_2e88b694-f21f-4864-a0a3-caba4a9c3bd2` |
| `consignacion_liquida_856d8192-abff-4328-ab0f-1309524bf46c` | 💸Liquidación de Cobranza | `consignacion_studio.asdasd_gestion_de_co_88278ad2-f6f7-4c48-8310-e11bc1c5f103` |
| `consignacion_comisio_f49e9ecf-d1bb-4638-8cf0-449827770acb` | 🧾Comisión Por Lote | `consignacion_studio.asdasd_gestion_de_co_88278ad2-f6f7-4c48-8310-e11bc1c5f103` |

Menús padre (en `consignacion_studio`): `asdasd_22e514c6…`, `asdasd_facturas_bc9a5af3…`, `asdasd_contactos_2e88b694…`, `asdasd_gestion_de_co_88278ad2…`

---

## 6. Vistas (`ir.ui.view`)

### 6.1 Vistas propias (modelo / nombre técnico del registro)

| Modelo | Views |
|---|---|
| `x_liquidacion_de_cobra` | list: `default_list_view_fo_c8b150c7-480c-4e79-9fd1-08cd7dd6c09c` · form: `default_form_view_fo_ac714850-8a2d-47d8-8f63-f6a523ab1053` + `odoo_studio_default__4699d948-be5e-4acb-922c-7f957a76b709` · search: `default_search_view__2ba010a5-a3a2-4ba2-b755-346840caac35` |
| `x_comision_por_lote` | list: `default_list_view_fo_1f2315ce-84f7-479a-82f0-af8ce2fd7c62` · form: `default_form_view_fo_74ac6b55-8ca2-45db-82e8-05d1e3f42545` + `odoo_studio_default__b5802a1b-ec53-45d6-8734-3c04119f0b2a` · search: `default_search_view__fc0835e0-4c0c-4c02-9e98-20ab40e075f0` |
| `x_comision_por_lote_line_4fbf2` | list: `default_list_view_fo_41d2e761-ed40-4843-afd9-a84bd404bd76` · form: `default_form_view_fo_2a693ceb-04f5-4dce-ae56-959d5dad2828` · search: `default_search_view__7f8edbb5-b111-4787-9a09-693a11aab393` |
| `x_comision_por_lote_line_bfd8a` | list: `default_list_view_fo_a4d9feec-40cf-405d-a9a6-801e78820236` · form: `default_form_view_fo_b3513a97-12c9-4fd0-9a2c-ad2e733abadf` · search: `default_search_view__f8974a03-2acc-4255-992e-cab056addcea` |

### 6.2 Vistas de `consignacion_studio` (referenciadas/heredadas)

| Nombre técnico | Modelo |
|---|---|
| `consignacion_studio.odoo_studio_stock_lo_684d1984-c0e5-4898-8794-ff2ec710da66` | `stock.location` |
| `consignacion_studio.default_form_view_fo_d12a378d-40da-4653-8858-471079089d54` | `x_perdidas_sc` |
| `consignacion_studio.odoo_studio_default__cddb8b6c-5ae0-48db-bf28-20008d8bbea8` | `x_lertas_de_reabas_sc` |
| `consignacion_studio.default_form_view_fo_58a1841f-e1b2-4c2f-b319-1d886c9a70f9` | `x_lertas_de_reabas_sc` |
| `consignacion_studio.default_form_view_fo_81945d3f-c85c-49df-8aae-1dac92d31a62` | `x_asignar_personal_sc` |
| `consignacion_studio.odoo_studio_sale_ord_4e0c5339-cc51-4af0-9d19-ff930630f42c` | `sale.order` |
| `consignacion_studio.default_form_view_fo_e4900968-e068-4d12-b505-f8fbef62374c` | `x_gestion_de_devolucio_sc` |
| `consignacion_studio.odoo_studio_default__9976f5a2-0e20-4421-950e-5e6440c85ed8` | `x_test_sc` |
| `consignacion_studio.default_form_view_fo_ef6ee0de-4db4-481c-90ad-7f01a2f3ce97` | `x_test_sc` |

### 6.3 Otras vistas propias (extensiones sobre modelos estándar)

| Nombre técnico | Modelo | Hereda de |
|---|---|---|
| `sale.view_sale_order_pivot` | `sale.order` | — |
| `odoo_studio_default__6812d009-e2eb-488a-85a1-bc628962f8d4` | `stock.location` | (kanban por defecto) |
| `odoo_studio_default__db309c87-de6c-4d5a-bc7c-73aecd10142a` | `x_perdidas_sc` | `consignacion_studio.default_form_view_fo_d12a378d…` |
| `odoo_studio_product__ead1faaf-4a54-4f44-ac34-3a5fff1184b2` | `product.template` | `product.product_template_kanban_view` |
| `odoo_studio_default__3aef28d5-ba23-4a73-ae19-6af17e9b4848` | `x_gestion_de_devolucio_sc` | `consignacion_studio.default_form_view_fo_e4900968…` |
| `odoo_studio_purchase_983969b0-d392-402c-9aac-f3a3eb2f41eb` | `purchase.order` | `purchase.purchase_order_form` |
| `odoo_studio_default__4d81adc8-1342-4fd6-aa7a-b579811b2167` | `x_asignar_personal_sc` | `consignacion_studio.default_form_view_fo_81945d3f…` |
| `odoo_studio_account__c5e2a9ba-f174-4ba7-94c1-ea5e78fccc9d` | `account.move` | `account_followup.view_followup_invoice_list` |
| `odoo_studio_mrp_prod_11449a7c-f77c-492c-8383-bc7c44f68153` | `mrp.production` | `mrp.mrp_production_form_view` |

---

## 7. Automatizaciones (`base.automation`)

| Nombre técnico | Nombre | Modelo | Disparador |
|---|---|---|---|
| `consignacion_studio.auto_llenar_producto_f5e0d049-fb29-47aa-a78f-7a24888fb158` | Autocompletar productos en oferta | `x_gestion_de_devolucio_sc` | on_change |
| `consignacion_studio.procesar_validacion__216650f7-0b46-435c-8ff0-f39ec088d726` | Validación del PIN del proceso | `x_validador_de_pin_sc` | on_create |
| `generar_referencia_d_4ce47c17-05c6-465b-a7ba-79b693040240` | Generar Referencia de Liquidación | `x_liquidacion_de_cobra` | on_create |
| `cargar_operaciones_a_cb24d082-eee6-4f36-b885-117f1dcbc5ad` | Cargar Operaciones Automáticamente | `x_liquidacion_de_cobra` | on_change |
| `aplicar_recargo_de_f_f5e48cdd-ecd3-4b23-bb83-96332971bc67` | Aplicar Recargo de Flete al Precio | `sale.order` | on_change |
| `bloquear_fabricacion_a9a2a3d4-18a5-4276-80e7-b5d923eb7540` | Generar Compras (Al Confirmar) | `mrp.production` | on_create |
| `bloquear_negativos_6f863382-3fcb-4a5b-af34-bd9aad2631cf` | Bloquear Ventas Negativas | `sale.order` | on_create_or_write |
| `el_bloqueo_al_finali_4203c6c8-4437-4eab-8491-bf5f001905ba` | El Bloqueo (Al Finalizar) | `mrp.production` | on_create_or_write |

---

## 8. Accesos a modelo (`ir.model.access`)

| Nombre técnico | Grupo | Modelo |
|---|---|---|
| `liquidacion_de_cobra_4883f0b8-bd7b-4085-ae66-c53ee871ba1f` | `base.group_system` | `x_liquidacion_de_cobra` |
| `liquidacion_de_cobra_bc1b3268-49d4-40bb-a784-642e851ac2f4` | `base.group_user` | `x_liquidacion_de_cobra` |
| `comision_por_lote_gr_d9328d08-9bc7-4b70-ac80-e5f5b27336ec` | `base.group_system` | `x_comision_por_lote` |
| `comision_por_lote_gr_e782ca59-2c0f-4daa-9071-282897a6b443` | `base.group_user` | `x_comision_por_lote` |
| `comision_por_lote_li_a9f64210-65dd-435f-9d6c-952383e28494` | `base.group_system` | `x_comision_por_lote_line_4fbf2` |
| `comision_por_lote_li_010e1a75-6590-4144-9399-d97bf4e7c094` | `base.group_user` | `x_comision_por_lote_line_4fbf2` |
| `comision_por_lote_li_58035b42-2e15-4155-90e2-48bbb41c6cd9` | `base.group_system` | `x_comision_por_lote_line_bfd8a` |
| `comision_por_lote_li_fa0e9a85-2334-442b-9344-66d3e606733b` | `base.group_user` | `x_comision_por_lote_line_bfd8a` |

---

## 9. Filtros (`ir.filters`)

| Nombre técnico | Nombre | Modelo |
|---|---|---|
| `proveedores_da98480f-85fe-45d2-b9bf-74ecfd929afb` | Facturas Clientes | `sms.account.code` |

---

## 10. Valores por defecto (`ir.default`)

| Nombre técnico | Campo | Valor |
|---|---|---|
| `activo_liquidacion_d_c96b64c2-7224-4259-9b8b-a9cb1d726cf9` | `x_active` | `true` |
| `secuencia_liquidacio_b8b203ee-8173-4668-8818-7ea149d66b7b` | `x_studio_sequence` | `10` |
| `barra_de_estado_de_f_87460cd9-25fe-4ca7-b426-ee61a7d1e258` | `x_studio_selection_field_2r6_1k3s2b7q3` | `Borrador` |
| `secuencia_comision_p_26788d48-e27d-4323-87b7-86bfea05a804` | `x_studio_sequence` | `10` |
| `barra_de_estado_de_f_13328152-f74c-4c1d-8c3d-6b498ad6e467` | `x_studio_selection_field_632_1k464f74e` | `Borrador` |

---

## 11. Registros no exportados (referencia de `warnings.txt`)

| Registro | Modelo | Campo |
|---|---|---|
| `odoo_studio_default__6812d009-e2eb-488a-85a1-bc628962f8d4` | `ir.ui.view` | `inherit_id` |
| `cancelar_e2c3f52e-d561-49b1-809a-3d66a71f1865` | `ir.actions.server` | `selection_value` |
| `proveedores_da98480f-85fe-45d2-b9bf-74ecfd929afb` | `ir.filters` | `action_id` |

---

## 12. Acciones/vistas referenciadas no exportadas

| Nombre técnico | Tipo |
|---|---|
| `consignacion_studio.validacion_c24db260-ca10-46cb-891d-1fa3601464f8` | ir.actions.server (Validar Pérdida) |
| `consignacion_studio.enviar_notificacion__caa644d6-dbfb-4d01-b55e-234cd3394368` | ir.actions.server (Enviar) |
| `consignacion_studio.confirmar_reabasteci_51ed5f7f-efad-4c70-a337-d2da70ca6248` | ir.actions.server (Registrar Solicitud) |
| `consignacion_studio.rma_marcar_recibido_4d852fdc-7efa-4950-8a88-8b5241c656aa` | ir.actions.server (Producto Recibido) |
| `consignacion_studio.rma_enviar_al_provee_4a46e0c4-aa6b-4da4-a335-1096d3c8b87f` | ir.actions.server (Enviar al Proveedor) |
| `consignacion_studio.rma_crear_nota_de_cr_5c3e4305-37b9-4be5-bcd6-e1c1c1d87532` | ir.actions.server (Finalizar Reembolso) |
| `consignacion_studio.abrir_nota_de_credit_7efff096-7d53-4c54-894e-abd1f56a798a` | ir.actions.server (Ver Nota de Crédito) |
